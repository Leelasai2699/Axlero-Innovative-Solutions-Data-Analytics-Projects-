# Snowflake warehouse and raw data layer

This setup creates a small, auto-suspending Snowflake warehouse, a `METRIC_MIND` database, and a `RAW` schema for the project CSVs. Raw business fields are loaded as `VARCHAR` so source values (including the `DD-MM-YYYY` dates) are not implicitly reformatted; each row also records its staged filename and load timestamp.

## Load the source CSVs

1. Connect to Snowflake with a role that can create warehouses, databases, schemas, stages, tables, and load data. The SQL uses an X-Small warehouse; adjust it if your account policy requires a different size.
2. In SnowSQL, upload each local file to the internal stage. Replace `<project-folder>` with the full local project path:

   ```sql
   PUT 'file://<project-folder>/Data/sales_transactions.csv' @METRIC_MIND.RAW.CSV_STAGE AUTO_COMPRESS=FALSE OVERWRITE=TRUE;
   PUT 'file://<project-folder>/Data/customers.csv' @METRIC_MIND.RAW.CSV_STAGE AUTO_COMPRESS=FALSE OVERWRITE=TRUE;
   PUT 'file://<project-folder>/Data/products.csv' @METRIC_MIND.RAW.CSV_STAGE AUTO_COMPRESS=FALSE OVERWRITE=TRUE;
   PUT 'file://<project-folder>/Data/metric mind date_dimension.csv' @METRIC_MIND.RAW.CSV_STAGE AUTO_COMPRESS=FALSE OVERWRITE=TRUE;
   ```

   `PUT` is a SnowSQL client command and must be run from SnowSQL, not a Snowflake worksheet. Quote the complete local file URI, especially when the project path contains spaces.
3. Run [`01_raw_layer.sql`](01_raw_layer.sql) in a Snowflake worksheet or with SnowSQL. It creates the warehouse/database/schema, CSV format, stage and raw tables, then loads all four staged files.
4. Review the final row-count query in the script. Snowflake's `COPY` load history skips files it has already loaded into each target table. If you intentionally need to reload unchanged files, use `FORCE = TRUE` on the relevant `COPY INTO` statement after considering duplicate rows.

## Objects created

- Warehouse: `METRIC_MIND_WH` (X-Small, auto-resumes, suspends after 60 seconds idle)
- Database and schema: `METRIC_MIND.RAW`
- Internal stage: `METRIC_MIND.RAW.CSV_STAGE`
- Tables: `RAW_SALES_TRANSACTIONS`, `RAW_CUSTOMERS`, `RAW_PRODUCTS`, and `RAW_DATE_DIMENSION`

No account identifiers, credentials, or secrets are stored in this project.
