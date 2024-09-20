# 10th September

# Data Analysis Report

## Data Format

The data is structured in JSON format with multiple entries. Each entry contains information about network flows captured by the system. The key elements of each entry are as follows:

- `flow`: Contains detailed information about the network flow.
- `interface`: The network interface through which the flow was captured.
- `internal`: Indicates if the flow is internal.
- `type`: The type of flow event (e.g., `flow_dpi_update`, `flow_dpi_complete`, `flow_stats`).

## Flow Types

### Flow DPI Update and Complete

- **flow_dpi_update**: Indicates the start of data capture for a flow.
- **flow_dpi_complete**: Indicates the completion of data capture for a flow.

### Flow Stats

- **flow_stats**: Provides updates on the number of new packets that have arrived for a particular digest.

### Flow Purge

- **flow_purge**: Indicates that the connection has ended.

## Unique Identifier

- **digest**: A unique ID for each connection.

## Example Data Structure

```json
[
    {
        "flow": {
            "category": {
                "application": 27,
                "domain": 0,
                "network": 0,
                "protocol": 22
            },
            "detected_application": 10033,
            "detected_application_name": "netify.netify",
            "detected_protocol": 196,
            "detected_protocol_name": "HTTP/S",
            "detection_guessed": false,
            "detection_packets": 6,
            "detection_updated": true,
            "dhc_hit": true,
            "digest": "b3ea28521dfe0a5f9ee6974dd8a290383ed22905",
            "dns_host_name": "backend.netify.ai",
            "fhc_hit": false,
            "first_seen_at": 1725613387050,
            "host_server_name": "agents.netify.ai",
            "ip_nat": false,
            "ip_protocol": 6,
            "ip_version": 4,
            "last_seen_at": 1725613387644,
            "local_bytes": 1537,
            "local_ip": "10.1.1.69",
            "local_mac": "f8:94:c2:d2:2e:54",
            "local_origin": true,
            "local_packets": 9,
            "local_port": 37612,
            "local_rate": 1537.0,
            "other_bytes": 4104,
            "other_ip": "148.113.141.168",
            "other_mac": "56:3b:d9:53:4d:0e",
            "other_packets": 5,
            "other_port": 443,
            "other_rate": 4104.0,
            "other_type": "remote",
            "soft_dissector": false,
            "ssl": {
                "alpn": [
                    "h2",
                    "http/1.1"
                ],
                "cipher_suite": "0x1301",
                "client_sni": "agents.netify.ai",
                "server_ja3": "f4febc55ea12b31ae17cfb7e614afda8",
                "version": "0x0303"
            },
            "total_bytes": 5641,
            "total_packets": 14,
            "vlan_id": 0
        },
        "interface": "wlp3s0",
        "internal": true,
        "type": "flow_dpi_update"
    }
]
```

## Summary

- **Flow DPI Update and Complete**: Start and complete data capture for a flow.
- **Flow Stats**: Update on new packets for a digest.
- **Flow Purge**: Connection ended.
- **Digest**: Unique ID for each connection.
