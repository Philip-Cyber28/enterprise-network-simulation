DHCP Configuration
1. Objective

Automatically assign IPv4 configuration to client devices using DHCP services.

2. Implementation

The DHCP server is configured to automatically distribute IP addresses and network settings to clients across multiple VLANs. DHCP pools are configured for the required departments, and DHCP relay is used where necessary to forward client requests to the DHCP server.

3. DHCP Scope Information

The DHCP pools are configured for the different VLANs and departments. Each pool provides the appropriate IP address range and network configuration to its clients.

VLAN	Network	Default Gateway	DNS Server	Address Pool
Department VLANs	As configured	As configured	As configured	As configured
4. Configuration

The DHCP pools are configured under Services > DHCP on the Packet Tracer server.

The following screenshots show the DHCP pool configuration and DHCP relay settings:

DHCP pool configuration: /Screenshots/it-dhcp-pool.png
DHCP pool details: /Screenshots/dhcp-pool-config.png
DHCP helper configuration: /Screenshots/dhcp-helper-cs.png
5. Verification

DHCP configuration was verified by checking whether client devices from different departments successfully received IP addresses from the DHCP server.

The following screenshots demonstrate the verification process:

IT department DHCP verification: /Screenshots/verify-dhcp-it.png
HR department DHCP verification: /Screenshots/verify-dhcp-hr.png
Administration department DHCP verification: /Screenshots/verify-dhcp-admin.png
Finance department DHCP verification: /Screenshots/verify-dhcp-finance.png
Sales department DHCP verification: /Screenshots/verify-dhcp-sales.png
Management department DHCP verification: /Screenshots/verify-dhcp-management.png
Guest department DHCP verification: /Screenshots/verify-dhcp-guest.png
DHCP server IP verification: /Screenshots/verify-dhcp-server-ip.png
6. Testing Results

DHCP verification was performed across the different department VLANs. The client verification screenshots document the DHCP testing process and the server IP verification screenshot documents the DHCP server configuration.

7. Screenshots

The following screenshots are included as evidence of DHCP implementation and testing:

/Screenshots/it-dhcp-pool.png
/Screenshots/dhcp-pool-config.png
/Screenshots/dhcp-helper-cs.png
/Screenshots/verify-dhcp-it.png
/Screenshots/verify-dhcp-hr.png
/Screenshots/verify-dhcp-admin.png
/Screenshots/verify-dhcp-finance.png
/Screenshots/verify-dhcp-sales.png
/Screenshots/verify-dhcp-management.png
/Screenshots/verify-dhcp-guest.png
/Screenshots/verify-dhcp-server-ip.png
