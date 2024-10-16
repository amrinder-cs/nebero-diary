# 26th September

## Daily Log - 26th September

### Changes Made

- Separated methods into `Utils.cpp` and `Utils.h`.
- Updated `Makefile` to incorporate the changes.
- Renamed `sent` to `data_sent` and `received` to `data_received`.

### Details

#### Makefile
- Added `src/Utils.cpp` to `SRC`.
- Added `build/Utils.o` to `OBJ`.
- Added rule for `build/Utils.o`.

#### arm_build.sh
- Removed old `arm_build` directory and created a new one.

#### Utils.cpp and Utils.h
- Moved relevant methods and definitions from `socket_client.cpp` to `Utils.cpp` and `Utils.h`.
- Added `processArguments` function to handle command-line arguments.
- Added `processConfig` function to handle configuration file reading and writing.
- Added `DatabaseConfig` struct to hold database configuration details.
- Declared `processArguments` and `processConfig` functions.
- Modified `processConfig` function to use the new `Config` struct.
- Added `socket_client_path` to the configuration.
- Replaced `DatabaseConfig` struct with `Config` struct.
- Added `socket_client_path` and `socket_server_path` to the `Config` struct.

#### socket_client.cpp
- Updated includes and removed moved methods.
- Defined `flush_bool` and `flowMap` as extern.
- Removed inline argument processing and configuration file handling.
- Integrated `processArguments` and `processConfig` functions.
- Updated to use the new `Config` struct.
- Configured the `.sock` file path using the new configuration.

### Segregated database config and config file reading. It's now in `Utils.h` and `Utils.cpp`. Makes the code more understandable.

- Created a new struct for `Config`, which can be useful for future configuration additions.



