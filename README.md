# Pharma Commercial Data Lake

A pharmaceutical commercial data lake built on **Azure Databricks** with **Unity Catalog**, implementing a Medallion architecture (Bronze → Silver → Gold) to ingest, transform, and aggregate commercial pharma data for business intelligence and sales analytics.

---

## Architecture Overview

```
Azure ADLS Gen2 (source-cdl)
        │
        ▼
  UC Volume: /Volumes/cdl/bronze/landing_files/   ← JSON source files
        │
        ▼
 ┌─────────────────────────────────────────────┐
 │              BRONZE LAYER (cdl.bronze)       │  Raw ingested data + audit metadata
 │  call_activity_bronze                        │
 │  hcp_master_bronze                           │
 │  product_master_bronze                       │
 │  rx_transactions_bronze                      │
 │  territory_master_bronze                     │
 └──────────────────┬──────────────────────────┘
                    │
                    ▼
 ┌─────────────────────────────────────────────┐
 │              SILVER LAYER (cdl.silver)       │  Cleaned, typed, deduplicated
 │  call_activity_silver                        │
 │  hcp_master_silver                           │
 │  product_master_silver                       │
 │  rx_transactions_silver                      │
 │  territory_master_silver                     │
 └──────────────────┬──────────────────────────┘
                    │
                    ▼
 ┌─────────────────────────────────────────────┐
 │              GOLD LAYER (cdl.gold)           │  Business aggregations + views
 │  brand_weekly_performance                    │
 │  hcp_engagement                              │
 │  territory_performance                       │
 │  call_rx_correlation                         │
 │  product_master_gold                         │
 │  vw_brand_weekly_performance (view)          │
 │  vw_hcp_engagement (view)                    │
 └─────────────────────────────────────────────┘
                    │
                    ▼
 ┌─────────────────────────────────────────────┐
 │        Commercial Performance Dashboard      │  Lakeview dashboard
 └─────────────────────────────────────────────┘
```

**Audit Layer:** `cdl.audit.ingestion_load_log` — tracks every file ingested by the bronze pipeline.

---

## Infrastructure

| Component | Value |
| --- | --- |
| Cloud | Azure |
| Storage Account | `datalakedevesh` |
| Source Container | `source-cdl` |
| Destination Container | `destination-cdl` |
| Unity Catalog | `cdl` |
| Schemas | `bronze`, `silver`, `gold`, `audit` |
| Landing Volume | `/Volumes/cdl/bronze/landing_files/` |

---

## Source Data

Source files are JSON, date-stamped, and named using the convention:

```
{entity_name}_{YYYY_MM_DD}.json
```

| Entity | Example File |
| --- | --- |
| call_activity | `call_activity_2026_06_15.json` |
| hcp_master | `hcp_master_2026_06_15.json` |
| product_master | `product_master_2026_06_15.json` |
| rx_transactions | `rx_transactions_2026_06_15.json` |
| territory_master | `territory_master_2026_06_15.json` |

---

## Project Structure

```
pharma_commercial_data_lake/
├── README.md
├── code/
│   ├── infra_setup              # One-time catalog/schema setup
│   ├── config_variables         # Shared path & catalog config (sourced via %run)
│   ├── p01_bronze_ingestion     # Bronze ingestion framework
│   ├── p02_silver_transformations  # Silver cleaning & deduplication framework
│   ├── p03_gold_aggregations    # Gold aggregation tables
│   ├── bronze_control_log_observability  # Audit log creation & observability queries
│   ├── delta_lake_concepts      # Delta Lake exploration (time travel, restore, history)
│   ├── pyspark_basics           # PySpark fundamentals (select, filter, schema, alias)
│   ├── validation_query         # SQL: count failed ingestion records
│   ├── new_data_ingested_query  # SQL: track newly ingested data
│   └── enhancements.md          # Backlog & enhancement checklist
├── gold_views/
│   ├── vw_brand_weekly_performance  # View with call completion rate & Rx per HCP
│   ├── vw_hcp_engagement            # View with HCP segmentation logic
│   ├── call_rx_correlation          # Query: call-to-Rx correlation gold table
│   ├── ingestion_log_tracking       # Query: audit log success tracking
│   └── query_history                # Ad-hoc query history
└── dashboards/
    ├── 01_KPI_Summary               # Overall KPI rollup query
    ├── 02_Brand_Weekly_Performance  # Weekly brand performance query
    └── Commercial Performance Dashboard  # Lakeview dashboard
```

---

## Notebooks

### `infra_setup`
One-time setup notebook to create and drop Unity Catalog schemas (`cdl.bronze`, `cdl.silver`, `cdl.gold`, `cdl.audit`).

---

### `config_variables`
Shared configuration notebook. Sourced into other notebooks via `%run`. Defines catalog names, schema names, volume paths, and ADLS cloud paths.

---

### `p01_bronze_ingestion`
**Bronze Ingestion Framework** — the main ingestion pipeline.

Key responsibilities:
- **File discovery:** Scans the landing volume for `.json` files using `discover_source_files()` and parses entity name + date from the filename using `parse_source_file_name()`.
- **Schema contracts:** Enforces per-entity column definitions via a `schema_contracts` dictionary (column names, data types, nullability).
- **Audit metadata:** Adds `bronze_load_ts`, `source_file_name`, `source_file_path`, `ingestion_file_date`, `ingestion_batch_id` columns to every record.
- **Duplicate check:** Skips files already loaded based on the audit log.
- **Write:** Saves Delta tables to `abfss://destination-cdl@datalakedevesh.dfs.core.windows.net/bronze/{entity}/` and registers them in `cdl.bronze`.
- **Audit logging:** Writes a record per file to `cdl.audit.ingestion_load_log` with status, row count, timestamps, and any error message.

---

### `p02_silver_transformations`
**Silver Transformation Framework** — cleans and standardises bronze data.

Key responsibilities:
- **Entity-level cleaning functions:** `clean_hcp_master`, `clean_product_master`, `clean_territory_master`, `clean_call_activity`, `clean_rx_transactions` — apply `trim`, `upper`, `initcap`, `to_date` type casting per column.
- **Deduplication:** Window function (`ROW_NUMBER`) partitioned by primary keys, ordered by `effective_date`, `ingestion_file_date`, `bronze_load_ts`; keeps only the latest record per key.
- **Row hash:** SHA-256 hash over key columns (`sha2 + concat_ws`) for change detection.
- **Write:** Saves Delta tables to `abfss://destination-cdl@.../silver/{entity}_silver/` and registers in `cdl.silver`.

**Entity configuration** (`silver_entity_config`) drives the processing loop with bronze table, silver table, storage path, primary keys, dedup order columns, and hash columns per entity.

---

### `p03_gold_aggregations`
**Gold Aggregation Layer** — produces business-ready analytical tables.

| Gold Table | Description |
| --- | --- |
| `brand_weekly_performance` | Weekly Rx volume, HCP count, calls and completed calls per brand and therapy area, joined from `rx_transactions_silver` + `product_master_silver` + `call_activity_silver` |
| `hcp_engagement` | Per-HCP call metrics (total, completed, planned, cancelled, avg duration) joined with Rx totals and territory data |
| `territory_performance` | Aggregated call and Rx metrics per sales territory |
| `call_rx_correlation` | Correlation between rep call activity and Rx prescription volume |

`write_gold_table(df, table_name, write_mode)` is a reusable utility that writes a DataFrame to the gold Delta location and registers it in `cdl.gold`.

---

### `bronze_control_log_observability`
Sets up and queries the audit schema. The `cdl.audit.ingestion_load_log` table tracks:

| Column | Description |
| --- | --- |
| `ingestion_batch_id` | UUID per pipeline run |
| `source_entity` | Entity name (e.g. `call_activity`) |
| `source_file_name` / `source_file_path` | Origin file |
| `source_file_date` | Date parsed from filename |
| `target_table_name` / `target_table_path` | Bronze Delta table destination |
| `write_mode` | `overwrite` / `append` |
| `row_count` | Records written |
| `load_status` | `success` / `failed` |
| `load_start_ts` / `load_end_ts` | Timing |
| `error_message` | Populated on failure |

---

### `delta_lake_concepts`
Exploration notebook for Delta Lake features using `call_activity_bronze` as the working example:
- `DESCRIBE HISTORY` — view table version history
- `SELECT ... VERSION AS OF n` — time travel reads
- `RESTORE TABLE ... VERSION AS OF n` — point-in-time restore

---

### `pyspark_basics`
PySpark fundamentals reference notebook using `call_activity` data:
- Reading JSON with inferred and manual schemas (`StructType`)
- `select`, column aliases, derived columns (e.g. `duration_minutes / 60`)
- `filter` with string expressions, `col()` conditions, and numeric predicates
- Writing Delta tables to ADLS and registering them in Unity Catalog

---

## Gold Views

Located in `gold_views/`, these SQL queries create or query analytical views on top of the gold tables.

| View / Query | Purpose |
| --- | --- |
| `vw_brand_weekly_performance` | Adds `call_completion_rate` and `rx_per_prescribing_hcp` computed metrics on top of `brand_weekly_performance` |
| `vw_hcp_engagement` | Adds `call_completion_rate` and an `hcp_segment` label (`High Value Engaged`, `High RX / Low Call`, `Engaged / Low RX`, `Low Engagement`) on top of `hcp_engagement` |
| `call_rx_correlation` | Direct query on the `call_rx_correlation` gold table |
| `ingestion_log_tracking` | Queries `cdl.audit.ingestion_load_log` for successfully loaded files |

---

## Dashboard

The **Commercial Performance Dashboard** (Lakeview) is built on two queries in `dashboards/`:

| Query | Description |
| --- | --- |
| `01_KPI_Summary` | Total prescriptions, total/completed calls, overall call completion rate, brand count, therapy area count, latest week |
| `02_Brand_Weekly_Performance` | Week-over-week brand performance: Rx volume, calls, completion rate, Rx per prescribing HCP |

---

## Enhancements Backlog

See [`code/enhancements.md`](#file-876982030259854) for the full checklist. Key planned improvements include:

**Bronze**
- Centralize config into a `get_config()` function
- Modularize ingestion into a `run_bronze_ingestion()` driver
- Log skipped files to the audit table
- Data quality and schema validation checks
- Auto Loader incremental ingestion
- Actual `MERGE INTO` upsert pattern

**Silver**
- Centralize config into `get_silver_config()`
- Create a `run_silver_processing()` driver function
- Reusable DQ validation framework
- Referential integrity checks (HCP, product, territory foreign keys)
- Silver audit log table

---

## Execution Order

To run the pipeline end-to-end:

1. **`infra_setup`** — run once to create schemas
2. **`p01_bronze_ingestion`** — ingest source JSON → bronze Delta tables
3. **`p02_silver_transformations`** — clean bronze → silver Delta tables
4. **`p03_gold_aggregations`** — aggregate silver → gold Delta tables
5. **`gold_views/vw_*`** — create or refresh analytical views
6. **Dashboard** — refresh the Commercial Performance Dashboard
