# 18th September

## Daily Log - 18th September

### Changes Made

- Updated `Makefile` to support compilation on older systems such as Debian 11.
    - Added `-std=c++17` to `CXXFLAGS`.
    - Included `build/socket_client.o` in `OBJ`.
    - Added rule for compiling `build/socket_client.o`.
- Updated `README.md` to include installation instructions for required packages.
- Modified `install.sh` to provide additional instructions for sourcing `.bashrc`.
