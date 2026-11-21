# Architecture

| Layer | Schema | Purpose |
|---|---|---|
| Raw | RAW | Source-shaped CSV landing tables and customer change events |
| Staging | STAGING | Trim, normalize and deduplicate latest records |
| Analytics | ANALYTICS | Customer/product dimensions and order fact |
| Control | CONTROL | Audit and orchestration objects |

Data flow: CSV -> internal stage -> RAW -> STAGING views -> ANALYTICS.
Customer changes can be captured by a Snowflake Stream and processed by a SQL
procedure invoked by a Task.

This is an educational starter. For production, add robust orchestration, batch IDs,
quarantine/error handling, recovery strategy, role-based access, CI/CD, monitoring,
and automated tests. Validate all scripts in your own Snowflake account.
