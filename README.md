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
##### 1. Physical and Logical Setup
Use Connections (lightning icon):
  * PC0 FastEthernet0 → Switch Fa0/2 (Copper Straight-Through)
  * PC1 FastEthernet0 → Switch Fa0/3 (Copper Straight-Through)
  * Server FastEthernet0 → Switch Fa0/4 (Copper Straight-Through)
  * Router G0/0 → Switch Fa0/1 (Copper Straight-Through)
Rule: if you use the wrong cable, the link lights won’t go green and your “network troubleshooting” becomes fake.
  <img width="1178" height="463" alt="image" src="https://github.com/user-attachments/assets/49d7c9fa-282e-4e17-af08-3fdcde8ba90f" />


##### 2. Router Configuration (Default Gateway)
The router was configured to act as the LAN gateway.

##### Key actions:
Click the router → CLI → then enter:
  * Assigned IP address 192.168.10.1/24 to the LAN interface.
  * Enabled the interface using no shutdown.
  * Verified interface status.
This gateway allows LAN devices to communicate outside their subnet.


### 3. Server Configuration (DNS and DHCP)
##### Static IP Configuration
Click Server → Desktop → IP Configuration:
 * IP: 192.168.10.10
 * Subnet Mask: 255.255.255.0
 * Default Gateway: 192.168.10.1
 * DNS: 192.168.10.10
   <img width="1434" height="584" alt="image" src="https://github.com/user-attachments/assets/d87614eb-71ba-4051-ad2c-9afb048b0053" />

#### DNS Setup
Server → Services → DNS:
 * DNS service enabled
 * Created name records such as:
 * 
    * intranet.local → 192.168.10.10
    <img width="1441" height="559" alt="image" src="https://github.com/user-attachments/assets/63aaaf71-af67-4fef-a609-a7f128a4c82f" />

#### DHCP Setup
Server → Services → DHCP:
  * DHCP service enabled
  * Address pool: 192.168.10.100 – 192.168.10.200
  * Default Gateway: 192.168.10.1
  * DNS Server: 192.168.10.10
    <img width="1917" height="714" alt="image" src="https://github.com/user-attachments/assets/4a78550b-039f-43b3-b034-5b1e47c3d720" />


### 4. Client Configuration
PC → Desktop → IP Configuration → click DHCP
All PCs were configured to obtain IP settings automatically using DHCP.
Each client successfully received:
  * Valid IP address
  * Correct subnet mask
  * Correct default gateway
  * Correct DNS server
    <img width="1665" height="610" alt="image" src="https://github.com/user-attachments/assets/14079d75-b472-497f-a353-13c25d0a8420" />

# Network Verification & Testing

### IP Verification
##### Using Command Prompt on each PC:
    ipconfig
Confirmed DHCP assignment and correct network parameters.
   <img width="1687" height="675" alt="image" src="https://github.com/user-attachments/assets/2c858c96-9556-473c-9b97-cecd6b3bc1e7" />


### Connectivity Testing (PING)
Tests performed in logical order:
  * PC → own IP (local stack validation)
  * PC → default gateway (router reachability)
  * PC → server (LAN communication)
  * PC → other PCs (switching functionality)
    <img width="1920" height="1029" alt="image" src="https://github.com/user-attachments/assets/a76846fa-03a4-4e95-98b7-49c552ff0748" />

### DNS Testing
    ping intranet.local
Successful name resolution confirmed DNS functionality.
   <img width="968" height="345" alt="image" src="https://github.com/user-attachments/assets/1d9b31c8-cb10-4548-a810-ffb26072de74" />

### LAN vs WAN (Applied Understanding)
#### LAN
  * Internal private network
  * Devices communicate through a switch
  * Router provides default gateway services
#### WAN
  * Connects LAN to external networks
  * Requires routing and proper gateway configuration
  * Simulated using an additional router and network segment

I implemented routing logic to ensure traffic could leave the LAN and return correctly.


# Common Network Issues and Solutions

#### Issue 1: Wrong IP Address (Wrong Subnet)
 * Break it: On PC0 set Static IP to 192.168.20.50 /24
 * Result: Can’t ping 192.168.10.1
#### Fix: switch back to DHCP or set correct static:
 * IP: 192.168.10.50
 * Gateway: 192.168.10.1
 * DNS: 192.168.10.10

#### Issue 2: Wrong Default Gateway
 * Break it: Set PC gateway to 192.168.10.254
 * Result: Can ping local PCs, but routing fails (no “outside subnet” access)
#### Fix: Set gateway back to 192.168.10.1

#### Issue 3: Wrong DNS Server
 * Break it: Set DNS on PC0 to 1.1.1.1 (no internet in this lab)
 * Result: ping 192.168.10.10 works, ping intranet.local fails
#### Fix: Set DNS back to 192.168.10.10

#### Issue 4: DHCP Not Assigning IP
 * Break it: Turn DHCP Service Off on the Server
 * Result: PC gets no IP (or a wrong fallback)
#### Fix: Turn DHCP back On and confirm pool settings are correct.

