# 16th September

## Daily Log - 13th September

### Makefile Creation

- Defined the compiler:
    ```makefile
    CXX = g++
    ```

- Set compiler flags:
    ```makefile
    CXXFLAGS = -I src -I /usr/include/cppconn
    ```

- Set linker flags:
    ```makefile
    LDFLAGS = -L /usr/lib -lmysqlcppconn
    ```

- Specified source and object files:
    ```makefile
    SRC = src/socket_client.cpp src/DatabaseManager.cpp
    OBJ = build/DatabaseManager.o
    ```

- Defined the target executable and directories:
    ```makefile
    TARGET = build/socket_client
    BUILD_DIR = build
    INSTALL_DIR = /opt/netifytodb
    ```

- Created the default rule:
    ```makefile
    all: $(BUILD_DIR) $(TARGET)
    ```

- Added rule for linking the executable:
    ```makefile
    $(TARGET): $(OBJ)
            $(CXX) -o $@ src/socket_client.cpp $(OBJ) $(LDFLAGS)
    ```

- Added rule for compiling object files:
    ```makefile
    build/DatabaseManager.o: src/DatabaseManager.cpp
            $(CXX) -c $< -o $@ $(CXXFLAGS)
    ```

- Created rule to create the build directory:
    ```makefile
    $(BUILD_DIR):
            mkdir -p $(BUILD_DIR)
    ```

- Added rule to install the executable:
    ```makefile
    install: $(TARGET)
            mkdir -p $(INSTALL_DIR)
            cp $(TARGET) $(INSTALL_DIR)/netifytodb
    ```

- Added rule to clean up build artifacts:
    ```makefile
    clean:
            rm -rf $(BUILD_DIR)
    ```

- Defined phony targets:
    ```makefile
    .PHONY: all clean install
    ```
