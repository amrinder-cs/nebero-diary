# 6th September Diary Entry

## Netify Information

### Command to Start Netify
To start Netify, use the following command:
```sh
netifyd -R -v -t -r -I wlp3s0
```

### Local and Other Nomenclature
The local designation indicates the endpoint's local side, and the other designation is indicated by the `other_type` field. These designations do not indicate a flow's direction. To determine which side of a flow started the conversation, consult the `local_origin` field. When this field is true, it indicates that the local endpoint started transmitting first. When false, the opposite endpoint started the flow.

#### Example
```json
"local_origin": true,
"local_ip": "192.168.4.105",
"local_bytes": 2434,
"other_type": "remote",
"other_ip": "31.13.80.53",
"other_bytes": 6139
```
In this example, `192.168.4.105` transmitted `2434` bytes and received `6139` bytes from `31.13.80.53`. The flow originated from `192.168.4.105`.

#### Summary
- `local_bytes` = Transmitted
- `other_bytes` = Received
- `"local_origin": true` = Traffic originating from the inside

## Flow Stats Information

### Description
Some network flows are long-lived, for example, audio/video streams and VPN connections. The Netify Agent will periodically publish a `flow_stats` record to the Data Stream. The network status on active flows provides real-time insights into the network.

### Example Use Cases
- Live bandwidth statistics
- QoE based on live data usage

#### Example
```json
"type": "flow_stats",
"flow": {
    "digest": "178bf5650a79d5e8ddc6a988d0c02b3d799180d0",
    "last_seen_at": 1606232131756,
    "local_bytes": 2434,
    "local_packets": 21,
    "other_bytes": 6139,
    "other_packets": 16,
    "total_bytes": 8573,
    "total_packets": 37
}
```