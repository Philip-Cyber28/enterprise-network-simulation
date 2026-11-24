# Network Topology

## 1. Objective
Document the physical and logical layout of the enterprise network.

## 2. Network Overview
The network is organized into an edge/WAN section, a core network, department access switches, and a server network.

## 3. Device Roles
| Device | Role |
|---|---|
| ISP router | Simulates the external service provider |
| R1 – Edge router | Connects the enterprise network to the ISP; performs edge functions configured in the project |
| R2 – Core router | Provides the router-to-core connection and routing functions configured in the project |
| Core Layer 3 switch | Provides Layer 3 switching and VLAN gateway functions |
| Access switches | Connect end-user devices and carry assigned VLANs |
| Server switch | Connects internal servers |
| Servers | Provide configured network services |

## 4. Physical Connections
Document the actual interfaces and links used.

| From device/interface | To device/interface | Link purpose |
|---|---|---|
| [Device/interface] | [Device/interface] | [WAN / routed / trunk / access] |
| [Device/interface] | [Device/interface] | [Purpose] |

## 5. Verification
- Check link status in Packet Tracer.
- Use `show ip interface brief` on routers and Layer 3 switches.
- Use `show cdp neighbors` where supported.

## 6. Screenshots
Add the final topology screenshot: `../Screenshots/01-Network-Topology.png`.
