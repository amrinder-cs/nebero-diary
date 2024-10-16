# 12th September
## Daily Log - 12th September

- Created paths automatically if they didn't exist.
- Added logging for database connections.
- Parameterized database queries.
- Configured credentials to be read from a config file instead of being hardcoded.

## Details:
Utilized the `nhollman/json` library to read configuration settings from a JSON file.

### Implementation: Reading from JSON in C++
```cpp
#include <iostream>
#include <fstream>
#include <nlohmann/json.hpp>

using json = nlohmann::json;

int main() {
    // Open the JSON file
    std::ifstream config_file("config.json");
    if (!config_file.is_open()) {
        std::cerr << "Could not open the config file!" << std::endl;
        return 1;
    }

    // Parse the JSON file
    json config;
    config_file >> config;

    // Read values from the JSON object
    std::string db_host = config["database"]["host"];
    int db_port = config["database"]["port"];
    std::string db_user = config["database"]["user"];
    std::string db_password = config["database"]["password"];

    // Output the values to verify
    std::cout << "Database Host: " << db_host << std::endl;
    std::cout << "Database Port: " << db_port << std::endl;
    std::cout << "Database User: " << db_user << std::endl;
    std::cout << "Database Password: " << db_password << std::endl;

    return 0;
}
```
