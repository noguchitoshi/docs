- When a table's locality is set to [`REGIONAL BY ROW`](set-locality.html), changefeed jobs targeting that table will fail.
- Changefeeds only work on tables with a single [column family](column-families.html) (which is the default for new tables).
- Changefeeds do not share internal buffers, so each running changefeed will increase total memory usage. To watch multiple tables, we recommend creating a changefeed with a comma-separated list of tables.
- Many DDL queries (including [`TRUNCATE`](truncate.html) and [`DROP TABLE`](drop-table.html)) will cause errors on a changefeed watching the affected tables. You will need to [start a new changefeed](create-changefeed.html#start-a-new-changefeed-where-another-ended).
- Changefeeds cannot be [backed up](backup.html) or [restored](restore.html).
- Partial or intermittent sink unavailability may impact changefeed stability; however, [ordering guarantees](stream-data-out-of-cockroachdb-using-changefeeds.html#ordering-guarantees) will still hold for as long as a changefeed [remains active](stream-data-out-of-cockroachdb-using-changefeeds.html#monitor-a-changefeed).
- Changefeeds cannot be altered. To alter, cancel the changefeed and [create a new one with updated settings from where it left off](create-changefeed.html#start-a-new-changefeed-where-another-ended).
- Additional target options will be added, including partitions.
- When an [`IMPORT INTO`](import-into.html) statement is run, changefeed jobs targeting that table will fail.
- Using a [cloud storage sink](create-changefeed.html#cloud-storage-sink) only works with `JSON` and emits [newline-delimited json](http://ndjson.org) files.
- Currently, [changefeeds](stream-data-out-of-cockroachdb-using-changefeeds.html) connected to [Kafka versions < v1.0](https://docs.confluent.io/platform/current/installation/versions-interoperability.html) are not supported.
- {{ site.data.products.enterprise }} changefeeds are currently disabled for [{{ site.data.products.serverless }} clusters](https://www.cockroachlabs.com/docs/cockroachcloud/quickstart). Core changefeeds are enabled.    