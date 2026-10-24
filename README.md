# Enterprise-Multi-Branch-Network-with-OSPF-VLANs-DHCP-STP-and-ACLs
Enterprise network design in Cisco Packet Tracer featuring OSPF, VLANs, inter-VLAN routing, DHCP, STP, ACLs, and redundant WAN links.
# Enterprise Multi-Branch Network Design

## Project Overview

This project demonstrates the design and configuration of a multi-branch enterprise network using Cisco Packet Tracer. It connects a main office and a branch through a redundant WAN topology using four routers.

The network implements VLAN segmentation, inter-VLAN routing, dynamic IP addressing, OSPF routing, Spanning Tree Protocol, and access control lists.

## Technologies Used

- Cisco Packet Tracer
- IPv4 addressing and subnetting
- VLANs and 802.1Q trunking
- Router-on-a-stick inter-VLAN routing
- DHCP
- OSPF routing (single area, Area 0)
- Spanning Tree Protocol (STP)
- Access Control Lists (ACLs)
- Serial WAN links
- Network connectivity testing and troubleshooting

## Network Topology

The network contains four routers connected in a square topology:

- **R0:** Main office gateway
- **R1 and R2:** Intermediate WAN routers
- **R3:** Branch router
- **CORE-SW1:** Main office core switch
- **ACC-SW1 and ACC-SW2:** Main office access switches
- **BR-SW1:** Branch access switch

The two WAN paths provide alternative routes between the main office and branch.

/screenshots/network-topology.png

## IP Addressing and VLANs

| Network | VLAN | Purpose | Gateway |
|---|---:|---|---|
| 192.168.10.0/24 | 10 | Sales | 192.168.10.1 |
| 192.168.20.0/24 | 20 | HR | 192.168.20.1 |
| 192.168.30.0/24 | 30 | Branch LAN | 192.168.30.1 |

### WAN Addressing

| WAN Link | Network | Endpoints |
|---|---|---|
| R0–R1 | 10.0.12.0/30 | R0: 10.0.12.1, R1: 10.0.12.2 |
| R0–R2 | 10.0.2.0/30 | R0: 10.0.2.1, R2: 10.0.2.2 |
| R1–R3 | 10.0.13.0/30 | R1: 10.0.13.1, R3: 10.0.13.2 |
| R2–R3 | 10.0.23.0/30 | R2: 10.0.23.1, R3: 10.0.23.2 |

## Key Configurations

### VLANs and Inter-VLAN Routing
VLAN 10 separates Sales traffic from VLAN 20 for HR. Router-on-a-stick enables routing between the two VLANs.

### DHCP
DHCP pools dynamically assign IP addresses to clients on the main office and branch LANs. Gateway addresses and reserved ranges are excluded from dynamic allocation.

### OSPF
OSPF Area 0 exchanges routes between the four routers. The redundant WAN paths allow routing through either intermediate router when the routing topology permits it.

### STP
Spanning Tree Protocol helps prevent Layer 2 switching loops. The core switch is configured with a lower STP priority for the main office VLANs to influence root bridge election.

### ACL Security
An extended ACL on R0 is intended to block ICMP traffic from the HR subnet (192.168.20.0/24) to the branch subnet (192.168.30.0/24), while permitting other IP traffic covered by the subsequent permit statement.

## Verification and Testing

Use the screenshots folder to document actual test results, including:

- OSPF neighbor adjacencies
- OSPF-learned routes
- VLAN and trunk configuration
- DHCP address assignment
- Successful connectivity between permitted networks
- ACL behavior for allowed and denied traffic

Only mark a test as successful after verifying it in Packet Tracer.

## Repository Structure

```text
enterprise-multibranch-network-ospf-vlans/
├── README.md
├── enterprise-multibranch-network.pkt
├── configs/
│   ├── R0.txt
│   ├── R1.txt
│   ├── R2.txt
│   ├── R3.txt
│   ├── CORE-SW1.txt
│   ├── ACC-SW1.txt
│   ├── ACC-SW2.txt
│   └── BR-SW1.txt
└── screenshots/
    ├── 01-network-topology.png
    ├── 02-ospf-routing.png
    ├── 03-ospf-neighbors.png
    ├── 04-vlan-configuration.png
    └── 05-connectivity-test.png
```

## How to Open the Project

1. Download `enterprise-multibranch-network.pkt`.
2. Open it using Cisco Packet Tracer.
3. Inspect the router and switch configurations.
4. Use the CLI to verify routing, VLANs, DHCP, STP, ACLs, and connectivity.

## Learning Objectives

- Design a multi-router enterprise network
- Configure and troubleshoot OSPF
- Implement VLAN segmentation and inter-VLAN routing
- Configure DHCP and extended ACLs
- Understand redundant WAN paths
- Verify network behavior using Cisco IOS commands

