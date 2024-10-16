# Daily Diary Log - September 30, 2024

- Added the `-lpthread` to `LDFLAGS` for ARM compatibility.
- Added dynamic updates for `user_id`. - As the user  logs in, it should update that info from the socket.
- Fetched IP - `user_id` from the database on startup.
- Updated to handle multiple IPs per username and ignore IPv6 by default.
- Moved functions `printPID`, `netifyDatabaseLogger`, and `runSocketServer` into `Utils.h`.
- Mapped IP with `user_id`.
- Fixed a bug related to accepting more data from the same client.

## Summary
Today's work focused on enhancing the functionality of the project by adding support for multiple IPs per username, dynamic updates of `user_id`, and ensuring compatibility with ARM by adding necessary flags. Additionally, several utility functions were refactored for better code organization.
