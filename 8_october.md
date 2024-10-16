# Daily Diary - 8th October 2024

## Summary of Work

### Changes Made
- Replaced `nhollman/json` with `RapidJson` by Tencent and added `rapidjson` source as a submodule.
- Abstracted methods used for processing JSON for better understanding.
- Made the socket listening configurable in the config file.

### Code Modifications
- **.gitmodules:** Added a new submodule for `rapidjson`.
- added user_id on flow start instead of flow flush, to preserve the user who started the flow.
- **Utils.cpp:** 
    - Updated JSON processing methods to use `RapidJson`.
    - Improved error handling and logging for JSON parsing.
    - Refactored functions to handle JSON data more efficiently.
- **Utils.h:** 
    - Included necessary headers for `RapidJson`.
    - Updated function signatures to use `RapidJson` types.
- **New Functionality:** 
    - Added a new function `processFlow` to handle flow data processing.
    - Introduced helper structures and methods to manage flow details and statistics.
    