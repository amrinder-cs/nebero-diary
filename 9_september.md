# 9th September

## Summary
On this day, I organized the codebase by segregating files into separate folders and added new functionality such as socket communication, data handling, JSON parsing, flow management, and debugging and logging.

## Changes Made
### Makefile Addition
- Added a `Makefile` to streamline the compilation process.

### File Organization
- Segregated files into separate folders to enhance code management and ease of working.

## Code Enhancements
### Socket Communication
- Implemented socket communication to connect to a Unix domain socket.
    ```cpp
    int socket_fd = socket(AF_UNIX, SOCK_STREAM, 0);
    ```

### Data Handling
- Added functionality to read data from the socket and process it based on the length header.
    ```cpp
    std::string header = readByteByByte(socket_fd);
    ```

### JSON Parsing
- Integrated JSON parsing to handle incoming data and extract relevant information.
    ```cpp
    json json_data = json::parse(data);
    ```

### Flow Management
- Enhanced flow management by checking if a flow exists in memory and updating or adding new flow information.
    ```cpp
    if (isFlow(json_data)) { ... }
    ```