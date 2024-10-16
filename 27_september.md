# 27th September

## Daily Log - 27th September


### Multithreading Implementation

#### socket_client.cpp
- Defined `SOCKET_SERVER_PATH` for the UNIX socket path.
- Added `runSocketServer` function to handle socket server operations.
- Created a new thread for `runSocketServer` in `main`.
- Updated `netifyDatabaseLogger` to handle data reading and parsing in a loop.
- Added CPU affinity settings for `runSocketServer` and `netifyDatabaseLogger` to bind them to specific CPU cores.
- Improved error handling and logging for socket operations.
- Integrated multithreading to listen and create a listener socket on different threads simultaneously.
- Updated the socket server to handle client connections and read data.
