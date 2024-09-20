
# Week 3 Summary

## Monday 26 August 2024

### Defeating DNS over HTTPS
- **Objective**: Analyze network traffic to determine data usage per website.
- **Challenges**: Installing network monitoring software on multiple devices in an enterprise.
- **Solution**: Intercept ClientHello messages to identify visited websites and log data usage.
- **Implementation**: Developed a lightweight C++ program to capture ClientHello messages.

## Tuesday 27 August 2024

### Extracting Server Name from ClientHello
- **Objective**: Log server name, source IP, bytes sent, and bytes received.
- **Method**: Parse TCP ClientHello packets using a custom C++ program.
- **Tools**: Wireshark for packet formatting reference.

## Wednesday 28 August 2024

### Connection Termination Handling
- **Objective**: Log data transfer upon connection termination.
- **Types of Termination**: FIN (graceful) and RST (abrupt).
- **Project Structure**: Split code into multiple files for better management.
- **Files**:
    ```
    .
    ├── build
    │   ├── DatabaseManager.o
    │   ├── main.o
    │   ├── packet_analyzer
    │   ├── PacketProcessor.o
    │   └── Utils.o
    ├── DatabaseManager.cpp
    ├── DatabaseManager.h
    ├── issues.md
    ├── main.cpp
    ├── Makefile
    ├── manager
    ├── PacketProcessor.cpp
    ├── PacketProcessor.h
    ├── Utils.cpp
    └── Utils.h
    ```

## Thursday 29 August 2024

### Database Migration and Compilation on ARM
- **Database Change**: Migrated from PostgreSQL to MySQL (MariaDB) for consistency with existing infrastructure.
- **New Database Class**:
    ```cpp
    class DatabaseManager {
    public:
            DatabaseManager(const string& host, const string& user, const string& password, const string& dbname);
            ~DatabaseManager();
            void executeQuery(const string& query);
    private:
            sql::Driver *driver;
            sql::Connection *con;
            string host;
            string user;
            string password;
            string dbname;
    };
    ```
- **ARM Compilation**: Set up an ARM virtual machine for cross-compilation.
- **Makefile Adjustment**:
    ```makefile
    LIB_DIRS = /usr/lib/*-linux-gnu
    ```

