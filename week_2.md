# Week 2

## Monday 19 August 2024

### Nat Punching using natpunchgo

- **Setup**: Created two virtual machines (alpine1 and alpine2) with NAT network in VirtualBox. Installed Wireguard on the main server and VMs.
- **Configuration**: Assigned IPs (10.66.66.1 for server, 10.66.66.2 for alpine1, and 10.66.66.3 for alpine2).
- **Compilation**: Compiled client and server scripts using Go.
- **Attempt 1**: Ran server and client scripts. Clients connected to the server but failed to discover each other.
- **Observation**: Running the client on the server itself allowed clients to resolve each other.

## Wednesday 21 August 2024

### Exploring Alternatives to natpunch

- **Issues with natpunch**: Not user-friendly and required significant resources to build a complete application.
- **Alternative**: Discovered Netbird, a Wireguard-based VPN provider using WebRTC and TURN protocol.
- **Setup**: Installed Netbird server on a homelab server using Docker and other tools. Successfully tested with Debian and Android clients.

## Friday 23 August 2024

### Network Bandwidth Usage Monitoring

- **Firewall Simulation**: Used a laptop as a firewall to monitor network traffic.
- **DHCP Issues**: Resolved IP assignment issues by assigning a static IP.
- **Gateway Configuration**: Configured the laptop as a gateway using iptables rules.
- **Testing**: Verified internet connectivity through the simulated firewall.
- **DNS and HTTPS**: Explored DNS caching issues and the unencrypted ClientHello in HTTPS requests.
- **Tools**: Identified Zeek and Suricata for network analysis based on ClientHello.

