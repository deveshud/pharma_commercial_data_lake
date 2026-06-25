| #  | Layer  | Checklist Item                                                                                                         | Status                           |
| -- | ------ | ---------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| 1  | Bronze | Create centralized `get_config()` function                                                                             | To Do                            |
| 2  | Bronze | Move all loose config variables inside `get_config()`                                                                  | To Do                            |
| 3  | Bronze | Create `discover_source_files(config)` function                                                                        | To Do                            |
| 4  | Bronze | Move `source_files` and `discovered_files` logic inside `discover_source_files()`                                      | To Do                            |
| 5  | Bronze | Update functions to accept `config` explicitly instead of relying on notebook-level variables                          | To Do                            |
| 6  | Bronze | Create main driver function `run_bronze_ingestion()`                                                                   | To Do                            |
| 7  | Bronze | Move duplicate-check + processing loop inside `run_bronze_ingestion()`                                                 | To Do                            |
| 8  | Bronze | Keep final execution cell minimal: `load_results = run_bronze_ingestion()`                                             | To Do                            |
| 9  | Bronze | Reorganize notebook sections: config, imports, contracts, utilities, framework functions, driver, validation           | To Do                            |
| 10 | Bronze | Remove temporary debug prints/displays                                                                                 | To Do                            |
| 11 | Bronze | Add docstrings/comments to core functions                                                                              | To Do                            |
| 12 | Bronze | Validate audit log after refactor                                                                                      | To Do                            |
| 13 | Bronze | Validate Bronze table row counts after refactor                                                                        | To Do                            |
| 14 | Bronze | Update README files with Bronze framework design, execution flow, table list, audit log, and known parked enhancements | To Do                            |
| 15 | Bronze | Prepare notebook for future Databricks Job scheduling                                                                  | Pending after project completion |
| 16 | Bronze | Log skipped files into audit table                                                                                     | Parked                           |
| 17 | Bronze | Validate missing/extra columns before ingestion                                                                        | Parked                           |
| 18 | Bronze | Bad-record / rejected-record handling                                                                                  | Parked                           |
| 19 | Bronze | Data quality checks                                                                                                    | Parked                           |
| 20 | Bronze | Move schema contracts to Delta config table                                                                            | Parked                           |
| 21 | Bronze | Move ingestion config to Delta config table                                                                            | Parked                           |
| 22 | Bronze | Archive processed source files                                                                                         | Parked                           |
| 23 | Bronze | Auto Loader incremental ingestion                                                                                      | Parked                           |
| 24 | Bronze | Actual `MERGE INTO` upsert pattern                                                                                     | Parked                           |
| 25 | Bronze | Retry/recovery strategy for failed files                                                                               | Parked                           |
| 26 | Bronze | Job-level alerting/notifications                                                                                       | Parked                           |
