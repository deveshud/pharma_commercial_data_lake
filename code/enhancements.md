|  # | Layer  | Checklist Item                                                                                                                    | Status                           |
| -: | ------ | --------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
|  1 | Bronze | Create centralized `get_config()` function                                                                                        | To Do                            |
|  2 | Bronze | Move all loose config variables inside `get_config()`                                                                             | To Do                            |
|  3 | Bronze | Create `discover_source_files(config)` function                                                                                   | To Do                            |
|  4 | Bronze | Move `source_files` and `discovered_files` logic inside `discover_source_files()`                                                 | To Do                            |
|  5 | Bronze | Update functions to accept `config` explicitly instead of relying on notebook-level variables                                     | To Do                            |
|  6 | Bronze | Create main driver function `run_bronze_ingestion()`                                                                              | To Do                            |
|  7 | Bronze | Move duplicate-check + processing loop inside `run_bronze_ingestion()`                                                            | To Do                            |
|  8 | Bronze | Keep final execution cell minimal: `load_results = run_bronze_ingestion()`                                                        | To Do                            |
|  9 | Bronze | Reorganize notebook sections: config, imports, contracts, utilities, framework functions, driver, validation                      | To Do                            |
| 10 | Bronze | Remove temporary debug prints/displays                                                                                            | To Do                            |
| 11 | Bronze | Add docstrings/comments to core functions                                                                                         | To Do                            |
| 12 | Bronze | Validate audit log after refactor                                                                                                 | To Do                            |
| 13 | Bronze | Validate Bronze table row counts after refactor                                                                                   | To Do                            |
| 14 | Bronze | Update README files with Bronze framework design, execution flow, table list, audit log, and known parked enhancements            | To Do                            |
| 15 | Bronze | Prepare notebook for future Databricks Job scheduling                                                                             | Pending after project completion |
| 16 | Bronze | Log skipped files into audit table                                                                                                | Parked                           |
| 17 | Bronze | Validate missing/extra columns before ingestion                                                                                   | Parked                           |
| 18 | Bronze | Bad-record / rejected-record handling                                                                                             | Parked                           |
| 19 | Bronze | Data quality checks                                                                                                               | Parked                           |
| 20 | Bronze | Move schema contracts to Delta config table                                                                                       | Parked                           |
| 21 | Bronze | Move ingestion config to Delta config table                                                                                       | Parked                           |
| 22 | Bronze | Archive processed source files                                                                                                    | Parked                           |
| 23 | Bronze | Auto Loader incremental ingestion                                                                                                 | Parked                           |
| 24 | Bronze | Actual `MERGE INTO` upsert pattern                                                                                                | Parked                           |
| 25 | Bronze | Retry/recovery strategy for failed files                                                                                          | Parked                           |
| 26 | Bronze | Job-level alerting/notifications                                                                                                  | Parked                           |
| 27 | Silver | Create centralized `get_silver_config()` function                                                                                 | To Do                            |
| 28 | Silver | Move all loose Silver config variables inside `get_silver_config()`                                                               | To Do                            |
| 29 | Silver | Update Silver functions to accept `config` explicitly instead of relying on notebook-level variables                              | To Do                            |
| 30 | Silver | Create main driver function `run_silver_processing()`                                                                             | To Do                            |
| 31 | Silver | Move entity processing loop inside `run_silver_processing()`                                                                      | To Do                            |
| 32 | Silver | Keep final Silver execution cell minimal: `silver_results = run_silver_processing()`                                              | To Do                            |
| 33 | Silver | Reorganize Silver notebook sections: config, imports, cleaning functions, reusable utilities, driver, validation                  | To Do                            |
| 34 | Silver | Remove temporary debug prints/displays from Silver notebook                                                                       | To Do                            |
| 35 | Silver | Add docstrings/comments to core Silver functions                                                                                  | To Do                            |
| 36 | Silver | Validate all Silver table locations after refactor                                                                                | To Do                            |
| 37 | Silver | Validate Silver table row counts after refactor                                                                                   | To Do                            |
| 38 | Silver | Validate duplicate counts for primary keys after refactor                                                                         | To Do                            |
| 39 | Silver | Update README files with Silver framework design, execution flow, table list, transformation rules, and known parked enhancements | To Do                            |
| 40 | Silver | Prepare Silver notebook for future Databricks Job scheduling                                                                      | Pending after project completion |
| 41 | Silver | Create reusable Silver validation / DQ framework                                                                                  | Parked                           |
| 42 | Silver | Add Silver validation summary table                                                                                               | Parked                           |
| 43 | Silver | Add Silver audit log table similar to Bronze audit log                                                                            | Parked                           |
| 44 | Silver | Add rejected-record handling for invalid/null/business-rule failed records                                                        | Parked                           |
| 45 | Silver | Create rejected-record Delta table for Silver failures                                                                            | Parked                           |
| 46 | Silver | Add referential integrity checks between fact and master tables                                                                   | Parked                           |
| 47 | Silver | Validate `call_activity_silver.hcp_id` against `hcp_master_silver.hcp_id`                                                         | Parked                           |
| 48 | Silver | Validate `call_activity_silver.product_id` against `product_master_silver.product_id`                                             | Parked                           |
| 49 | Silver | Validate `call_activity_silver.territory_id` against `territory_master_silver.territory_id`                                       | Parked                           |
| 50 | Silver | Validate `rx_transactions_silver.hcp_id` against `hcp_master_silver.hcp_id`                                                       | Parked                           |
| 51 | Silver | Validate `rx_transactions_silver.product_id` against `product_master_silver.product_id`                                           | Parked                           |
| 52 | Silver | Validate `rx_transactions_silver.territory_id` against `territory_master_silver.territory_id`                                     | Parked                           |
| 53 | Silver | Replace overwrite pattern with `MERGE INTO` upsert pattern                                                                        | Parked                           |
| 54 | Silver | Capture Silver row counts, rejected counts, duplicate counts, and load status                                                     | Parked                           |
| 55 | Silver | Move Silver entity config from Python dictionary to Delta config table                                                            | Parked                           |
| 56 | Silver | Move Silver transformation rules to config where possible                                                                         | Parked                           |
| 57 | Silver | Parameterize Silver write mode instead of hardcoding overwrite                                                                    | Parked                           |
| 58 | Silver | Add batch-level summary output for processed entities, row counts, and failures                                                   | Parked                           |
| 59 | Silver | Add retry/recovery strategy for failed Silver entities                                                                            | Parked                           |
| 60 | Silver | Add job-level alerting/notifications for Silver processing                                                                        | Parked                           |
|  61 | Gold  | Create centralized `get_gold_config()` function                                                                             | To Do  |
|  62 | Gold  | Move loose Gold config variables inside `get_gold_config()`                                                                 | To Do  |
|  63 | Gold  | Update Gold functions to accept `config` explicitly instead of relying on notebook-level variables                          | To Do  |
|  64 | Gold  | Create reusable `read_silver_tables(config)` function                                                                       | To Do  |
|  65 | Gold  | Create reusable `write_gold_table(config, df, table_name)` function                                                         | To Do  |
|  66 | Gold  | Create main driver function `run_gold_processing()`                                                                         | To Do  |
|  67 | Gold  | Move all Gold table build logic inside `run_gold_processing()`                                                              | To Do  |
|  68 | Gold  | Keep final Gold execution cell minimal: `gold_results = run_gold_processing()`                                              | To Do  |
|  69 | Gold  | Reorganize Gold notebook sections: config, imports, source reads, aggregation functions, write function, driver, validation | To Do  |
|  70 | Gold  | Remove temporary debug displays from Gold notebook                                                                          | To Do  |
|  71 | Gold  | Add docstrings/comments to Gold transformation functions                                                                    | To Do  |
|  72 | Gold  | Validate all Gold table locations after refactor                                                                            | To Do  |
|  73 | Gold  | Validate row counts for all Gold tables after refactor                                                                      | To Do  |
|  74 | Gold  | Validate `brand_weekly_performance` grain: one row per `week_start_date + product_id`                                       | To Do  |
|  75 | Gold  | Validate `hcp_engagement` grain: one row per `hcp_id`                                                                       | To Do  |
|  76 | Gold  | Validate `territory_performance` grain: one row per `territory_id`                                                          | To Do  |
|  77 | Gold  | Validate `call_rx_correlation` grain: one row per `week_start_date + hcp_id + product_id + territory_id`                    | To Do  |
|  78 | Gold  | Add duplicate-grain validation checks for all Gold tables                                                                   | To Do  |
|  79 | Gold  | Add null-check validation for key Gold dimensions                                                                           | To Do  |
|  80 | Gold  | Add Gold table row count summary query                                                                                      | To Do  |
|  81 | Gold  | Add Gold table freshness validation using `gold_load_ts`                                                                    | To Do  |
|  82 | Gold  | Add Gold validation SQL queries for dashboard/reporting use                                                                 | To Do  |
|  83 | Gold  | Update README with Gold table purpose, grain, source tables, and output paths                                               | To Do  |
|  84 | Gold  | Document business meaning of each Gold metric                                                                               | To Do  |
|  85 | Gold  | Document Gold lineage from Silver source tables                                                                             | To Do  |
|  86 | Gold  | Add Gold layer to final architecture diagram                                                                                | To Do  |
|  87 | Gold  | Prepare Gold notebook for future Databricks Job scheduling                                                                  | Done   |
|  88 | Gold  | Validate Gold notebook execution through Databricks Job                                                                     | Done   |
|  89 | Gold  | Add SQL Warehouse validation query for Gold table row counts                                                                | Done   |
|  90 | Gold  | Add SQL Warehouse validation query for Gold data load checks                                                                | Done   |
|  91 | Gold  | Add Gold audit log table similar to Bronze audit log                                                                        | Parked |
|  92 | Gold  | Capture Gold row counts, load status, start time, end time, and error message                                               | Parked |
|  93 | Gold  | Add batch-level summary output for processed Gold tables                                                                    | Parked |
|  94 | Gold  | Replace full overwrite pattern with incremental/upsert pattern where applicable                                             | Parked |
|  95 | Gold  | Add retry/recovery strategy for failed Gold table builds                                                                    | Parked |
|  96 | Gold  | Add job-level alerting/notifications for Gold failures                                                                      | Parked |
|  97 | Gold  | Add performance optimization using partitioning where useful                                                                | Parked |
|  98 | Gold  | Evaluate `OPTIMIZE` and `ZORDER` strategy for Gold tables                                                                   | Parked |
|  99 | Gold  | Add data quality thresholds for business metrics                                                                            | Parked |
| 100 | Gold  | Create Gold semantic/business views for dashboard users                                                                     | Parked |
| 101 | Gold  | Add metric definitions table for reusable KPI documentation                                                                 | Parked |
| 102 | Gold  | Add dashboard on top of Gold monitoring queries                                                                             | Parked |
| 103 | Gold  | Add data freshness dashboard for Bronze, Silver, and Gold                                                                   | Parked |
| 104 | Gold  | Add comparison checks between Silver source counts and Gold aggregate totals                                                | Parked |
| 105 | Gold  | Move Gold table configuration to Delta config table                                                                         | Parked |
| 106 | Gold  | Parameterize Gold write mode instead of hardcoding overwrite                                                                | Parked |
| 107 | Gold  | Add unit-style validation queries for each Gold table                                                                       | Parked |
| 108 | Gold  | Add business anomaly checks for sudden drops/spikes in calls or prescriptions                                               | Parked |
| 109 | Gold  | Add query history analysis for Gold SQL usage and dashboard performance                                                     | Parked |
| 110 | Gold  | Update final project README with orchestration, monitoring, and Gold outputs                                                | To Do  |
| 111| All | Add query history view for query performance management | To Do
