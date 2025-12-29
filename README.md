# Basic Network Setup and Troubleshooting (Cisco Packet Tracer)

### Overview
In this lab, I designed and implemented a functional small office network using Cisco Packet Tracer. The objective was to demonstrate hands-on understanding of LAN networking, IP addressing, DHCP, DNS, default gateways, basic routing, and troubleshooting common network issues.

Rather than only configuring a working network, I intentionally introduced common misconfigurations and resolved them to validate real-world troubleshooting skills.

### Tools Used
  * Cisco Packet Tracer
  * Router (Cisco 2911)
  * Switch (Cisco 2960)
  * End Devices (PCs)
  * Server (DNS and DHCP)

IP Addressing Scheme
LAN Network: 192.168.10.0/24

| Device       | IP Address                | Purpose         |
| ------------ | ------------------------- | --------------- |
| Router (LAN) | 192.168.10.1              | Default Gateway |
| Server       | 192.168.10.10             | DNS / DHCP      |
| PCs          | DHCP (192.168.10.100–200) | Client Devices  |

This structure reflects a realistic small-office LAN setup.

### Step-by-Step Implementation
#### 1. Physical and Logical Setup
  * Connected PCs and Server to the Switch using copper straight-through cables.
  * Connected the Switch to the Router using a straight-through cable.
  * Verified link lights to confirm physical connectivity.

#### 2. Router Configuration (Default Gateway)
The router was configured to act as the LAN gateway.

#### Key actions:
  * Assigned IP address 192.168.10.1/24 to the LAN interface.
  * Enabled the interface using no shutdown.
  * Verified interface status.
This gateway allows LAN devices to communicate outside their subnet.
