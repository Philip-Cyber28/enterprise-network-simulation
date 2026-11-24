# OSPF Configuration

## 1. Objective
Implement OSPF to dynamically exchange routing information between participating Layer 3 devices.

## 2. Implementation
Document the devices participating in OSPF, the OSPF process ID, areas, and networks advertised.

## 3. OSPF Details
| Device | Process ID | Area | Networks advertised |
|---|---|---|---|
| [Device] | [ID] | [Area] | [Networks] |

## 4. Configuration
Example syntax only; replace values with the actual configuration:

```cisco
router ospf [PROCESS-ID]
 network [NETWORK-ADDRESS] [WILDCARD-MASK] area [AREA-ID]
```

## 5. Verification
```cisco
show ip ospf neighbor
show ip protocols
show ip route ospf
show ip ospf interface brief
```

## 6. Testing Results
Record whether OSPF neighbors reached the expected state and whether remote routes appeared in the routing table.

## 7. Screenshots
Add OSPF neighbor and routing table screenshots.
