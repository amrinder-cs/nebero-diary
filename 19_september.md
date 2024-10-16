# 19th September

## Daily Log - 19th September

### Changes Made

- Fixed `/var/run/netifyd/netifyd.sock` path.
- Addressed unknown protocol issue by storing `NULL` (not possible because it's not nullable).
- Added application protocol ID.
- Created a reference table for application and categories.
- Implemented date change flush using `kill -SIGUSR1 $(cat /opt/netify-agent/var/run/netifyd/netifyd-db-sink.pid)`.
- Added `-v` flag to control console output.
- Renamed `local bytes` to `Uploaded`.
- Renamed `other bytes` to `Downloaded`.
- Renamed `FlowInfo` to `flow_info` and `sourceIP` to `source_ip`.

