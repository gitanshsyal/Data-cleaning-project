# Data-cleaning-project
Azure databricks data cleaning challenge-->

| Field         | Rule                                             | Source of validation |
| ------------- | ------------------------------------------------ | -------------------- |
| `CustomerID`  | Not null                                         | Inline               |
| `Name`        | Not null                                         | Inline               |
| `Email`       | Must not be empty and should contain “@”         | Inline               |
| `State`       | Must exist in `Valid_States` table in Azure SQL  | Lookup               |
| `CountryCode` | Must exist in `Valid_Country` table in Azure SQL | Lookup               |
| `Age`         | Not null and must be ≥ 18                        | Inline               |

👉 If a record fails any rule, it’s bad → goes to /files/discarded/
👉 If it passes all → goes to /files/source/

As part of this mini project, I designed and implemented a data validation and cleaning pipeline that automatically separates good and bad records before storing them into the Azure Data Lake.

Tech Stack Used
==================================================================

Azure Data Lake Gen2 – Storage

Azure SQL Database – Lookup tables

Azure Key Vault – Secret management

Azure Databricks (PySpark) – Data processing

JDBC Connector – For reading lookup data from Azure SQL

Steps I followed
==================================================================

Created required resources in Azure (Data Lake, SQL DB, Key Vault, Databricks).

Stored database credentials securely in Key Vault.

Loaded lookup tables (Valid_States, Valid_Country) from Azure SQL into Databricks using JDBC.

Read raw customer data from Data Lake.

Applied data quality checks using PySpark transformations.

Added a category column to classify records as target (good) or discarded (bad).

Wrote the processed data back to Data Lake partitioned by category.

