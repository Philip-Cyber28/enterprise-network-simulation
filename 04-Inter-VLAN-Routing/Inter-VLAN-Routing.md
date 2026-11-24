# Inter-VLAN Routing

## 1. Objective
Allow authorized communication between different VLANs using Layer 3 routing.

## 2. Implementation
Inter-VLAN routing is provided by the Layer 3 switch using switched virtual interfaces (SVIs), if this is how the final topology is configured.

## 3. Configuration
Example SVI syntax (replace addresses with the actual gateway addresses):

```cisco
configure terminal
ip routing
interface vlan 20
 ip address [GATEWAY-IP] 255.255.255.0
 no shutdown
end
```

Create an SVI for each VLAN that requires a gateway.

## 4. Verification
```cisco
show ip interface brief
show ip route
show vlan brief
```

## 5. Testing Results
Record successful and unsuccessful inter-VLAN tests, including any restrictions applied by ACLs.

## 6. Screenshots
Add SVI configuration and inter-VLAN ping screenshots.
