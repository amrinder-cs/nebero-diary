# Daily Diary - 4th October

# Changes

- **SQL Statements Buffer**: I added a buffer for SQL statements, which temporarily holds the data before it is flushed to the database. The default maximum buffer size is set to 50.
- **Configurable Buffer Size**: I introduced the ability to configure the `sql_statement_buffer_size` in our `db_config.json` file, allowing for more flexibility based on different use cases.
- **Signal Handler for Flushing**: I implemented a signal handler that flushes the buffer based on time. Specifically, sending the signal `kill -SIGUSR2` will trigger the data flush.

Additionally, I made an update to ensure that the server name is fetched and updated during `flow_dpi_update` or `flow_dpi_complete` events.

