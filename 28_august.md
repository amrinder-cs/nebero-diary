Wednesday Aug 28 2024

# Adding a connection terminate condition


an HTTPS connection can terminate in two ways:

- FIN (connection finished gracefully)
- RST (Reset, due to connection abruptly closing)


Both of them set flags in the network request.

Here's how fin and ACK are set:

![FIN_ACK](fin_ack.png)


Either it resets or it closes gracefully, we only care about flushing amount of data transferred when it shuts down to the database.
I realized the code had reached about 350 lines, and it would only grow. So instead of having just one file, i decided to split it into multiple files.


Here's the project structure now:

```bash
.
├── build
│   ├── DatabaseManager.o
│   ├── main.o
│   ├── packet_analyzer
│   ├── PacketProcessor.o
│   └── Utils.o
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

3 directories, 14 files
```

The makefile is made to make our compilation easier, i've set the compiler flags in it and added a build directory.

```bash
	┌─[root][THISPC][±][segregate ✓][~/ClientHello-Capture]
	└─▪  ./build/packet_analyzer 
	Usage: ./build/packet_analyzer <interface>
```
