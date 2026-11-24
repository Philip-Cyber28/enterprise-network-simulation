# Troubleshooting and Testing

## 1. Objective
Verify that the network operates as intended and document troubleshooting performed.

## 2. Connectivity Tests
| Test | Source | Destination | Expected result | Actual result |
|---|---|---|---|---|
| Same VLAN | [Client] | [Client] | [Pass/Fail] | [Result] |
| Inter-VLAN | [Client] | [Other VLAN] | [Pass/Fail] | [Result] |
| DHCP | [Client] | DHCP server | Valid lease | [Result] |
| DNS | [Client] | DNS hostname | Resolves correctly | [Result] |
| Web | [Client] | Web server | Page loads | [Result] |
| External network | [Client] | External test server | Reachable if configured | [Result] |
| ACL test | [Source] | [Destination] | Matches policy | [Result] |

## 3. Verification Commands
```cisco
show ip interface brief
show vlan brief
show interfaces trunk
show ip route
show ip ospf neighbor
show access-lists
show etherchannel summary
show spanning-tree
```

On PCs, use:
```text
ipconfig
ping [DESTINATION-IP]
tracert [DESTINATION-IP]
```

## 4. Troubleshooting Log
| Issue | Cause | Resolution |
|---|---|---|
| [Describe issue] | [Identified cause] | [Fix applied] |

## 5. Final Results
Summarize which tests passed, which failed, and any known limitations.

## 6. Screenshots
Add screenshots showing successful tests and relevant troubleshooting evidence.
