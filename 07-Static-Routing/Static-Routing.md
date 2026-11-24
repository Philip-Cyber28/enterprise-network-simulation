# Static Routing

## 1. Objective
Configure static or default routes to provide reachability between networks.

## 2. Implementation
Document which routers or Layer 3 devices use static routes and the purpose of each route.

## 3. Route Table
| Device | Destination network | Next hop / exit interface | Purpose |
|---|---|---|---|
| [Device] | [Network/prefix] | [Next hop] | [Purpose] |

## 4. Configuration
Example syntax (use the actual destination and next-hop values):

```cisco
ip route [DESTINATION-NETWORK] [SUBNET-MASK] [NEXT-HOP-IP]
```

Default route syntax:

```cisco
ip route 0.0.0.0 0.0.0.0 [NEXT-HOP-IP]
```

## 5. Verification
```cisco
show ip route
show ip route static
ping [DESTINATION-IP]
traceroute [DESTINATION-IP]
```

## 6. Testing Results
Record which remote networks were reachable through the configured routes.

## 7. Screenshots
Add routing table and connectivity screenshots.
