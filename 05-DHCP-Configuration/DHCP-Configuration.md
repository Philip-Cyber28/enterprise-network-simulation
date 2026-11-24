
# DNS and Server Services

## 1. Objective

Document the DNS service and other server services configured in the enterprise network. The DNS server provides hostname resolution, allowing client devices to access network services using hostnames instead of IP addresses.

## 2. Server Inventory

The enterprise network uses three servers connected to the Core Layer 3 Switch through Access Switch 3 (SW3). All servers belong to VLAN 10 (SERVER).

| Service | Server Name | IP Address | Default Gateway |
|---|---|---|---|
| WEB | Web Server | 192.168.10.10 | 192.168.10.1 |
| DNS | DNS Server | 192.168.10.20 | 192.168.10.1 |
| DHCP | DHCP Server | 192.168.10.30 | 192.168.10.1 |

### Server Network Information

- VLAN: 10 (SERVER)
- Network: 192.168.10.0/24
- Subnet Mask: 255.255.255.0
- Default Gateway: 192.168.10.1

## 3. DNS Configuration

The DNS service is configured on the Packet Tracer DNS server under **Services > DNS**.

The DNS server uses the static IP address `192.168.10.20` and default gateway `192.168.10.1`.

The DNS service provides hostname resolution for devices across the enterprise network.

### DNS Server Configuration

![Set DNS Server](/Screenshots/set-dns-server.png)

### DNS Host Records

The DNS server is configured to resolve hostnames to their corresponding server IP addresses.

| Hostname | Record Type | IP Address |
|---|---|---|
| Web Server hostname | A | 192.168.10.10 |

The A record maps the configured web server hostname to its IP address, allowing clients to access the web server using its hostname.

## 4. Other Server Services

The enterprise network includes the following server services:

### 4.1 Web Server

- Server IP Address: `192.168.10.10`
- Default Gateway: `192.168.10.1`
- VLAN: 10
- Network: `192.168.10.0/24`

The Web Server provides website hosting services for network clients.

### 4.2 DHCP Server

- Server IP Address: `192.168.10.30`
- Default Gateway: `192.168.10.1`
- VLAN: 10
- Network: `192.168.10.0/24`

The DHCP Server automatically assigns IPv4 configuration to client devices across the configured VLANs.

### 4.3 DNS Server

- Server IP Address: `192.168.10.20`
- Default Gateway: `192.168.10.1`
- VLAN: 10
- Network: `192.168.10.0/24`

The DNS Server translates configured hostnames into their corresponding IP addresses.

## 5. Verification

DNS configuration was verified by checking the DNS server settings and testing the DNS service.

The verification process includes:

- Confirming that clients receive the correct DNS server address (`192.168.10.20`).
- Checking the configured DNS host records.
- Testing hostname resolution using `nslookup` if supported.
- Accessing the configured website using its hostname in the PC web browser.
- Testing server reachability using `ping`.

### DNS Server Verification

![Verify DNS Server](/Screenshots/verify-dns-server.png)

## 6. Testing Results

DNS server configuration and verification were performed to ensure that hostname resolution is available within the enterprise network.

The DNS server uses the static IP address `192.168.10.20`, while the Web Server uses `192.168.10.10`.

The verification screenshot provides evidence of the DNS server configuration and testing process.

## 7. Network Connectivity

All three servers are connected to Access Switch 3 (SW3) and assigned to VLAN 10.

| No. | Switch | Interface | Connected Device | VLAN |
|---|---|---|---|---|
| 1 | SW3 | F0/1 | WEB Server | 10 |
| 2 | SW3 | F0/2 | DNS Server | 10 |
| 3 | SW3 | F0/3 | DHCP Server | 10 |

The servers communicate through the SERVER VLAN using the default gateway `192.168.10.1`.

## 8. Screenshots

The following screenshots are included as evidence of DNS configuration and verification:

1. `/Screenshots/set-dns-server.png`
2. `/Screenshots/verify-dns-server.png`
