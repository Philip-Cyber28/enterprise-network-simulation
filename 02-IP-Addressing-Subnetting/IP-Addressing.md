# IP Addressing and Subnetting

## 1. Objective
Document the IPv4 addressing plan used by the enterprise network.

## 2. Addressing Block
Private IPv4 address block: `192.168.0.0/16`

## 3. VLAN Addressing
The following allocation is based on the VLAN plan supplied for this project. Confirm that it matches the final Packet Tracer configuration.

| VLAN ID | Department | Network |
|---:|---|---|
| 10 | Server | 192.168.10.0/24 |
| 20 | IT | 192.168.20.0/24 |
| 30 | HR | 192.168.30.0/24 |
| 40 | Admin | 192.168.40.0/24 |
| 50 | Finance | 192.168.50.0/24 |
| 60 | Sales | 192.168.60.0/24 |
| 70 | Management | 192.168.70.0/24 |
| 80 | Guest | 192.168.80.0/24 |

## 4. Gateway and Host Addressing
| VLAN | Default gateway | DHCP range / static hosts |
|---|---|---|
| 10 | [Add gateway] | [Add range or server IPs] |
| 20 | [Add gateway] | [Add range] |
| 30 | [Add gateway] | [Add range] |
| 40 | [Add gateway] | [Add range] |
| 50 | [Add gateway] | [Add range] |
| 60 | [Add gateway] | [Add range] |
| 70 | [Add gateway] | [Add range] |
| 80 | [Add gateway] | [Add range] |

## 5. Point-to-Point Links
| Link | Network | Interface IPs |
|---|---|---|
| ISP–R1 | [Add subnet] | [Add IPs] |
| R1–R2 | [Add subnet] | [Add IPs] |
| R2–Core L3 switch | [Add subnet] | [Add IPs] |

## 6. Verification
- `show ip interface brief`
- `show ip route`
- `ipconfig` on end devices

## 7. Screenshots
Add addressing and subnet verification screenshots.
