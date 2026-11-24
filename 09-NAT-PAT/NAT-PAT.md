# NAT and PAT

## 1. Objective
Document address translation used to allow internal devices to communicate with the simulated external network.

## 2. Implementation
Identify the device performing NAT/PAT and the inside and outside interfaces.

## 3. NAT Details
| Item | Value |
|---|---|
| NAT device | [Device name] |
| Inside interface | [Interface] |
| Outside interface | [Interface] |
| Inside address range | [Private network(s)] |
| Translation method | [Dynamic NAT / PAT / Static NAT] |

## 4. Configuration
Document the actual NAT commands used. Example PAT syntax:

```cisco
access-list [NUMBER] permit [INSIDE-NETWORK] [WILDCARD-MASK]
ip nat inside source list [NUMBER] interface [OUTSIDE-INTERFACE] overload
```

Also document the `ip nat inside` and `ip nat outside` interface commands used.

## 5. Verification
```cisco
show ip nat translations
show ip nat statistics
```

Test access to the simulated external server.

## 6. Testing Results
Record whether internal clients reached the external network and whether translations were created.

## 7. Screenshots
Add NAT configuration, translation table, and connectivity screenshots.
