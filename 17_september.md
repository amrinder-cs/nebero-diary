# 17th September

## Daily Log - 17th September

### Changes Made

- Added `proc-core` in `install.sh`.
- Fixed `install.sh` to include a prompt for adding the binary path to `.bashrc`.
- Fixed a bug in `DatabaseManager.cpp` that caused the wrong time to be updated in the database.
- Updated `executePreparedStatement` method to remove the `firstSeenAt` parameter.
- Modified `flushToDatabase` function in `socket_client.cpp` to use `CURDATE()` instead of `FROM_UNIXTIME`.
- The bug was fixed by removing the `firstSeenAt` parameter from the `executePreparedStatement` method and the `flushToDatabase` function.
- Implementation details: Updated the `executePreparedStatement` method in `DatabaseManager.cpp` and `DatabaseManager.h` to remove the `firstSeenAt` parameter. Adjusted the `flushToDatabase` function in `socket_client.cpp` to use `CURDATE()` for the date field and updated the parameter list accordingly.