# 20th September

## Daily Log - 20th September

### Changes Made

- Added `arm_build.sh` script to automate building on ARM architecture.
- Updated `DatabaseManager` to include `executePreparedDebugStatement` method.
- Modified `FlowInfo` structure to include `unix_timestamp`.
- Implemented `flushToDatabaseDebug` function in `socket_client.cpp` to insert debug information into `netify_debug` table.
- Updated `flushToDatabaseAll` to call `flushToDatabaseDebug`.

#### `arm_build.sh`
```bash
#!/bin/bash
ssh fw "rm -fr ~/netify"
ssh fw "mkdir -p ~/netify/src"
rsync -av src/* root@fw:~/netify/src
scp Makefile root@fw:~/netify/
ssh fw "make -C ~/netify"
scp root@fw:~/netify/build/socket_client ./arm_build/
```
