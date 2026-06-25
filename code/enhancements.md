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