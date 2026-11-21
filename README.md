# Project 01 — Enterprise Retail Data Engineering with Snowflake

An intermediate learning project using fictional retail data to practise Snowflake SQL,
CSV ingestion, transformations, incremental MERGE patterns, SCD Type 2, Streams, Tasks,
and data-quality validation.

**Status:** Starter code drafted; validate each script in your Snowflake account before
calling the project complete or production-ready. All included records are synthetic.

## Architecture

```text
CSV files -> Internal stage -> RAW tables -> STAGING views
                                      |              |
                                      +----------> ANALYTICS dimensions/facts
RAW customer changes -> Stream -> SQL procedure -> SCD2 customer dimension
                                      |
                                      +----------> Tasks / orchestration
```

## Structure

- `sql/01_environment_setup.sql` — warehouse, database, schemas
- `sql/02_table_creation.sql` — raw, control, dimension and fact tables
- `sql/03_file_formats_stages.sql` — CSV format and internal stage
- `sql/04_data_ingestion.sql` — COPY INTO commands
- `sql/05_data_transformation.sql` — staging views and initial models
- `sql/06_incremental_loading.sql` — repeatable MERGE patterns
- `sql/07_scd_type_2.sql` — customer history tracking
- `sql/08_streams_tasks.sql` — change stream, procedure and task
- `sql/09_data_quality.sql` — data-quality checks
- `data/` — four synthetic CSV files
- `docs/architecture.md` — design notes
- `tests/validation_queries.sql` — validation queries

## Run order

1. Run SQL scripts 01, 02 and 03 in order.
2. Upload all four CSVs from `data/` to stage `RETAIL_DW.RAW.RETAIL_RAW_STAGE`.
3. Run scripts 04 through 09 in order. Read comments before running the Streams/Tasks demo.
4. Run `tests/validation_queries.sql`.

In Snowsight, open the internal stage and use **Upload Files**. Verify with:
`LIST @RETAIL_DW.RAW.RETAIL_RAW_STAGE;`

## Trial/cost precautions

The script creates an XSMALL warehouse with 60-second auto-suspend and initially suspended.
Use it only while running queries. Suspend it after each session:
`ALTER WAREHOUSE RETAIL_WH SUSPEND;`
Monitor trial credits and do not leave scheduled tasks running unattended.

## Expected sample counts

- Customers: 5
- Products: 5
- Orders: 6
- Order items: 10
- Sum of order-item extended values: 27,390.00

## Notes

Use a role with required object-creation privileges. Do not commit credentials, account
identifiers, personal data, or employer data. This starter is educational; production use
would require stronger orchestration, recovery, security, observability, and testing.
