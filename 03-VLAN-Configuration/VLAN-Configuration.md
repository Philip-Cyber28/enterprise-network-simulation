# VLAN Configuration

## 1. Objective
Implement VLAN segmentation to logically separate departments and server infrastructure within the enterprise network.

## 2. VLAN Allocation
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

## 3. Configuration
Document the commands used to create and name the VLANs. Example syntax:

```cisco
configure terminal
vlan 10
 name SERVER
vlan 20
 name IT
end
```

Repeat for the remaining VLANs using the names configured in the project.

## 4. Verification
```cisco
show vlan brief
show interfaces trunk
```

## 5. Testing Results
Record whether end devices were assigned to the correct VLANs and whether trunk links carried the required VLANs.

## 6. Screenshots
Add screenshots of VLAN creation, port assignments, and verification.
