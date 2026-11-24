# DHCP Configuration

## 1. Objective
Automatically assign IPv4 configuration to client devices.

## 2. Implementation
Document the DHCP server used, its static IP address, and the VLANs for which it provides addresses.

## 3. DHCP Scope Information
| VLAN | Network | Default gateway | DNS server | Address pool |
|---|---|---|---|---|
| [VLAN] | [Network] | [Gateway] | [DNS IP] | [Pool range] |

## 4. Configuration
Document the DHCP pools configured under **Services > DHCP** on the Packet Tracer server, or the IOS DHCP configuration if a router provides DHCP.

If using a remote DHCP server, document the relay configuration on each client VLAN interface:

```cisco
interface vlan [VLAN-ID]
 ip helper-address [DHCP-SERVER-IP]
```

## 5. Verification
- Set client devices to DHCP.
- Check the assigned address, mask, gateway, and DNS server.
- Use `ipconfig` on PCs.
- Use `show running-config` to inspect relay configuration.

## 6. Testing Results
Record which clients received valid leases and whether they could reach their gateway.

## 7. Screenshots
Add DHCP service/pool settings and client IP configuration screenshots.
