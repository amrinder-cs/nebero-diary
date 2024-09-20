
# Network Connection Management Diary - 3rd September

On the 3rd of September, I made several updates and improvements to my program that captures client hellos and maps them to the source port and target IP + hostname, then stores how many bytes were transferred. Here are the relevant changes:

- Refactored the code extensively to adhere to object-oriented programming standards.
- Introduced a `Packet` class for easier processing.
- Conducted simple tests to ensure the correct hostname was being inserted.

# Documentation for Network Connection Management Code

This code provides functionality for managing network connections, parsing TLS Client Hello messages, and storing connection information in a database. Below is a detailed explanation of the key components and functions in the code:

## Included Libraries
- `Utils.h`: Custom utility functions.
- `<iostream>`: Standard input/output stream objects.
- `<iomanip>`: Input/output manipulators.
- `<cctype>`: Character handling functions.
- `<cstdint>`: Fixed-width integer types.
- `<unordered_map>`: Unordered associative containers.
- `<map>`: Ordered associative containers.
- `DatabaseManager.h`: Custom database management class.

## Global Variables
- `std::unordered_map<uint64_t, ConnectionInfo> connectionMap`: Stores connection information indexed by a unique key.
- `std::map<uint64_t, bool> connection_state`: Stores the state of connections.
- `DatabaseManager db_manager`: Manages database connections and queries.

## Functions

### `bool is_utf8(const std::string& str)`
Checks if a given string is valid UTF-8.

### `void print_bytes(const u_char *data, size_t length)`
Prints the bytes of a given data array in hexadecimal format.

### `std::string bytes_to_string(const u_char *data, size_t length)`
Converts a byte array to a printable string, replacing non-printable characters with a dot (`.`).

### `std::string parse_client_hello(const u_char *tls_data, size_t length)`
Parses a TLS Client Hello message and extracts the Server Name Indication (SNI) if present.

### `Packet::Packet(struct ip ip_header, struct tcphdr tcp_header)`
Constructor for the `Packet` class, initializes packet information from IP and TCP headers.

### `uint32_t ipToInt(const std::string& ip)`
Converts an IP address string to a 32-bit integer.

### `uint64_t computeIndex(const std::string& srcIP, const std::string& tgtIP, uint16_t port)`
Computes a unique index for a connection based on source IP, target IP, and port.

### `void insertBytesInfo(const std::string& src_ip, int port, const std::string& dst_ip, bool fwd_connection, int bytes)`
Inserts or updates byte information for a connection in the `connectionMap`.

### `void deleteConnectionInfo(const std::string& src_ip, int port, const std::string& dst_ip)`
Deletes connection information from the `connectionMap`.

### `void displayHostnameInfo(std::string src_ip, int src_port, std::string dst_ip, int dst_port, std::string server_name)`
Displays connection information including the hostname.

### `void storeConnectionInfo(const std::string& src_ip, int port, const std::string& dst_ip)`
Stores connection information in the database.

### `void insertHostname(const std::string& src_ip, const std::string& dst_ip, int port, const std::string& hostname)`
Inserts or updates the hostname for a connection in the `connectionMap`.

## Usage
1. **Initialization**: Ensure that the `DatabaseManager` is properly initialized with the correct database connection parameters.
2. **Packet Handling**: Use the `Packet` class to initialize packet information from IP and TCP headers.
3. **Connection Management**: Use the provided functions to manage connection information, including inserting, updating, and deleting connection details.
4. **TLS Parsing**: Use `parse_client_hello` to extract SNI from TLS Client Hello messages.
5. **Database Operations**: Use `storeConnectionInfo` to store connection details in the database and `insertHostname` to update hostnames.
