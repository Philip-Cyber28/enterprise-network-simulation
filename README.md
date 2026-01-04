
# HOME NETWORK LAB - TECHNICAL DOCUMENTATION

Built a simulated enterprise network environment using virtualization
to practice and demonstrate IT infrastructure skills including network
configuration, security, Active Directory, and service deployment.

![Network Topology Diagram](Images/NetworkDiagram.png)

## 🎯​OBJECTIVES  
✓ Design and implement segmented network architecture  
✓ Configure enterprise-grade firewall rules  
✓ Deploy Windows Server with Active Directory Domain Services  
✓ Implement user/group management and access control  
✓ Configure file sharing with NTFS permissions  
✓ Deploy web services (IIS)  
✓ Automate configuration with Group Policy  
✓ Test and validate network security  

## 🖥️​TECHNOLOGIES USED  
- Virtualization: Oracle VirtualBox
- Firewall/Router: pfSense 2.8.0
- Operating Systems: 
  - Windows Server 2022 (Domain Controller)
  - Windows 10 Pro (Workstations)
  - Ubuntu 22.04 Desktop (Guest workstation)
- Services: Active Directory, DNS, IIS, File Sharing, Print Services
- Protocols: TCP/IP, DHCP, DNS, HTTP, SMB/CIFS

## 🛜​NETWORK CONFIGURATION  
**📂VLAN ARCHITECTURE** 

VLAN 10 - MANAGEMENT (192.168.10.0/24)  
- Purpose: IT administration and network management  
- Gateway: 192.168.10.1 (pfSense)  
- DHCP Range: .100-.200  
- DNS: 192.168.40.10 (DC01)  
- Access: Full access to all VLANs and services  
- Hosts: WIN10-MGMT  

VLAN 20 - USERS (192.168.20.0/24)
- Purpose: Employee workstations
- Gateway: 192.168.20.1 (pfSense)
- DHCP Range: .100-.200
- DNS: 192.168.40.10 (DC01)
- Access: Server VLAN + Internet (Blocked: Management, Guest)
- Hosts: WIN10-USER

VLAN 30 - GUEST (192.168.30.0/24)
- Purpose: Guest/visitor devices with restricted access
- Gateway: 192.168.30.1 (pfSense)
- DHCP Range: .100-.200
- DNS: 8.8.8.8 (Public DNS)
- Access: Internet only (Blocked: All internal networks)
- Hosts: Ubuntu-Guest

VLAN 40 - SERVER (192.168.40.0/24)
- Purpose: Infrastructure servers and services
- Gateway: 192.168.40.1 (pfSense)
- DHCP Range: .100-.200
- DNS: 192.168.40.10 (Self/DC01)
- Access: Accepts from Management & Users, can reach Internet
- Hosts: DC01 (192.168.40.10 - Static)

![pfSense Interface Assignments](Images/InterfaceAssignment.png)
*pfSense interface configuration showing all VLANs*  

![pfSense DHCP Leases](Images/DHCPLeases.png)  
*DHCP leases showing all VMs with their assigned IP addresses*

**⚙️PFENSE FIREWALL CONFIGURATION**

WAN Interface (em0):
- Type: NAT (connected to home network)
- Purpose: Internet connectivity for entire lab
- IP: DHCP from home router

LAN Interfaces:
- em1: LAN (192.168.1.0/24) - Not used
- em2: MANAGEMENT (192.168.10.1/24)
- em3: USERS (192.168.20.1/24)
- em4: GUEST (192.168.30.1/24)
- em5: SERVER (192.168.40.1/24)

NAT Configuration:
- Outbound NAT enabled on all interfaces
- All internal VLANs use WAN IP for internet access

**🧱FIREWALLL SUMMARY**

MANAGEMENT VLAN:  
- ✅PASS - Any protocol from MANAGEMENT net to Any destination  
    → Allows full administrative access

![Management Firewall Rules](Images/FirewallMGMT.png)
*Firewall rules for Management VLAN - full access*  

USERS VLAN:   
- 🚫BLOCK - Any protocol from USERS net to 192.168.10.0/24  
    → Prevents access to Management VLAN  
- 🚫BLOCK - Any protocol from USERS net to 192.168.30.0/24  
    → Prevents access to Guest VLAN  
- ✅PASS - Any protocol from USERS net to 192.168.40.0/24  
    → Allows access to Server VLAN  
- ✅PASS - Any protocol from USERS net to Any  
    → Allows Internet access
  
![Users Firewall Rules](Images/FirewallUSER.png)
*Firewall rules for Users VLAN - controlled access*  

GUEST VLAN:
- 🚫BLOCK - Any protocol from GUEST net to private networks   
    → Blocks all internal network access  
- ✅PASS - Any protocol from GUEST net to Any  
    → Allows Internet access only

![Guest Firewall Rules](Images/FirewallGUEST.png)
*Firewall rules for Guest VLAN - internet only*

SERVER VLAN:
- ✅PASS - Any protocol from 192.168.10.0/24 to SERVER net  
    → Accepts connections from Management  
- ✅PASS - Any protocol from 192.168.20.0/24 to SERVER net  
    → Accepts connections from Users  
- ✅PASS - Any protocol from SERVER net to Any  
    → Allows outbound Internet access

![Server Firewall Rules](Images/FirewallSERVER.png)
*Firewall rules for Server VLAN - accepting connections*  

Security Principle: Default Deny  
- All traffic not explicitly allowed is blocked  
- Implements principle of least privilege  
- Network segmentation enforced at firewall level  

## 🗃️ACTIVE DIRECTORY CONFIGURATION

**🆔DOMAIN INFORMATION**
- Domain Name: homelab.local
- NetBIOS Name: HOMELAB
- Domain Controller: DC01.homelab.local
- Forest Functional Level: Windows Server 2016
- Domain Functional Level: Windows Server 2016

![AD Users and Computers Overview](Images/OUList.png)
*Active Directory Organizational Unit structure*

**🖥️DOMAIN CONTROLLER SPECIFICATIONS**
- Hostname: DC01
- IP Address: 192.168.40.10 (Static)
- OS: Windows Server 2022 Standard Evaluation
- Roles Installed:
  - Active Directory Domain Services (AD DS)
  - DNS Server
  - IIS Web Server
  - File and Storage Services
  - Print and Document Services

**🏢ORGANIZATIONAL UNIT STRUCTURE**  

homelab.local
 - Departments
   - IT Staff
     - Users: jadmin, tuser
   - Sales
     - Users: ssales
   - HR  
     - Users: hhr
- Workstations
  - WIN10-MGMT
  - WIN10-USER
  - Servers
    - DC01

**👥USER ACCOUNTS**  

Administrator (Built-in)
- Description: Domain Administrator account
- Member of: Domain Admins, Enterprise Admins

jadmin (John Admin)
- OU: Departments/IT Staff
- Description: IT Administrator
- Member of: Domain Admins, IT Admins
- Purpose: Daily administrative tasks

tuser (Test User)
- OU: Departments/IT Staff
- Description: Standard IT user
- Member of: IT Admins
- Purpose: Testing standard user access
  
![AD Users - IT Staff OU](Images/ITUser.png)
*Users in IT Staff OU*

ssales (Sarah Sales)
- OU: Departments/Sales
- Member of: Sales Team
- Purpose: Sales department representative

![AD Users - Sales](Images/SalesUser.png)
*Users in Sales OU*

hhr (Helen HR)
- OU: Departments/HR
- Member of: HR Team
- Purpose: HR department representative

![AD Users - HR](Images/HRUser.png)
*Users in HR OU*

**👮SECURITY GROUPS**

IT Admins (Global Security Group)
- Location: Departments/IT Staff
- Members: jadmin, tuser
- Permissions: Full access to IT shared folder

Sales Team (Global Security Group)
- Location: Departments/Sales
- Members: ssales
- Permissions: Modify access to Sales shared folder

HR Team (Global Security Group)
- Location: Departments/HR
- Members: hhr
- Permissions: Modify access to HR shared folder

![Security Groups](Images/SecGroup.png)
*Security group*
![Group Membership](Images/GroupMembership.png)
*Example: jadmin group membership details*

**🤝DOMAIN-JOINED COMPUTERS**  

WIN10-MGMT
- OU: Workstations
- IP: 192.168.10.100 (DHCP)
- Purpose: IT management workstation
- Users: jadmin, Administrator

WIN10-USER
- OU: Workstations
- IP: 192.168.20.100 (DHCP)
- Purpose: Standard user workstation
- Users: tuser, ssales, hhr

![Workstations OU](Images/ADWorkstation.png)
*Domain-joined computers in Workstations OU*
![Servers OU](Images/ADServer.png)
*DC01 in Servers OU*

**🛠️DNS CONFIGURATION**

- Primary DNS Server: DC01 (192.168.40.10)
- Integrated with Active Directory
- Forward Lookup Zones: homelab.local
- Reverse Lookup Zones: Created automatically
- Forwarders: 8.8.8.8, 8.8.4.4 (for external resolution)
- DHCP configured to provide DC01 as DNS server

![DNS Manager](Images/DNSLookup.png)
*DNS Forward Lookup Zone for homelab.local*

## 👨‍🔧SERVICES CONFIGURATION

**🌐IIS WEB SERVER**

- Server: DC01 (192.168.40.10)
- Version: IIS 10.0
- Website: HomeLab Intranet
- URL: http://dc01.homelab.local or http://192.168.40.10
- Document Root: C:\inetpub\wwwroot
- Features: Static content, ASP.NET 4.8
- Access: Management and Users VLANs (Blocked from Guest)
- Purpose: Internal company portal demonstrating web services

![IIS Website - Homepage](Images/IISHomepage.png)
*Custom HomeLab Intranet website running on IIS*
![IIS Manager](Images/IISManager.png)
*IIS Manager showing website configuration*

**🗃️FILE SHARING SERVICES**

- Share Name: Shared
- UNC Path: \\DC01\Shared
- Physical Path: C:\Shared

![Mapped Drive](Images/MappedDrive.png)  
*S: drive automatically mapped via Group Policy*

**🗂️Folder Structure and Permissions**

Company (All employees)
- Path: \\DC01\Shared\Company
- NTFS: Domain Users (Read)
- Purpose: Company-wide documents

IT (IT Department)
- Path: \\DC01\Shared\IT
- NTFS: IT Admins (Full Control)
- Purpose: IT documentation and tools

Sales (Sales Department)
- Path: \\DC01\Shared\Sales
- NTFS: Sales Team (Modify)
- Purpose: Sales documents and reports

HR (HR Department)
- Path: \\DC01\Shared\HR
- NTFS: HR Team (Modify)
- Purpose: Confidential HR documents

![File Share Structure](Images/FileShareStruc.png)  
*File share structure: \\DC01\Shared with department folders*

**🔓Access Control Method**
- Share-level permissions: Domain Users (Read)
- NTFS permissions: Group-based
- Security: Inheritance disabled on department folders
- Principle: Least privilege access

![File Share - Access Granted](Images/AccessGranted.png)  
*Successful access to authorized folder (IT folder by IT user)*
![File Share - Access Denied](Images/AccessDenied.png)  
*Access denied to unauthorized folder - NTFS permissions working*

**🖨️PRINT SERVICES**

- Print Server: DC01
- Printer Name: HomeLab-Printer
- Type: Virtual (Print to File)
- Share Name: \\DC01\HomeLab-Printer
- Driver: Generic / Text Only
- Access: All domain users
- Purpose: Demonstrate print services management

![Print Management](Images/PrintManagement.png)  
*Print Management console showing HomeLab-Printer*

## 📜GROUP POLICY CONFIGURATION

**📢DEPLOYED GROUP POLICY OBJECTS**

Desktop Wallpaper Policy  
- Scope: Workstations OU
- Configuration: User Configuration
- Settings: Sets desktop wallpaper to Windows default
- Path: User Config > Admin Templates > Desktop > Desktop
- Purpose: Demonstrate GPO application

Map Shared Drive
- Scope: Domain-wide (homelab.local)
- Configuration: User Configuration (Preferences)
- Settings: Maps S: drive to \\DC01\Shared
- Reconnect: Yes
- Purpose: Automate drive mapping for all users

IT Desktop Shortcuts
- Scope: IT Staff OU
- Configuration: User Configuration (Preferences)
- Settings: Creates desktop shortcut to \\DC01\Shared\IT
- Purpose: Quick access to IT resources

![Group Policy Management](Images/GPOManagement.png)  
*Group Policy Management Console showing all GPOs*
![GPO - Drive Mapping](Images/GPOMappedDrive.png)  
*Drive mapping configuration in Group Policy Preferences*
![GPO - Desktop Shortcuts](Images/GPOShortcut.png)  
*Desktop shortcuts GPO configuration for IT Staff*  

**📝GPO APPLICATION PROCESS**  
- Computer policies apply at startup
- User policies apply at logon
- Update command: gpupdate /force
- Testing: gpresult /r (shows applied policies)

![GPResult Output](Images/GPResult.png)
*gpresult /r showing applied Group Policies*  

## ✍🏻TESTING & VALIDATION

**🛜NETWORK CONNECTIVITY TESTS**  
✓ All VMs receive DHCP addresses in correct ranges  
✓ DNS resolution working (nslookup, ping by hostname)  
✓ Internet access from all VLANs  
✓ Inter-VLAN routing through pfSense gateway 

![ipconfig Output](Images/IPConfig.png)  
*ipconfig /all showing correct IP, DNS, and gateway configuration*
![Successful DNS Resolution](Images/Nslookup.png)  
*nslookup successfully resolving dc01.homelab.local*

**🧱FIREWALL RULE VALIDATION**  
✓ Management can access all VLANs  
✓ Users can access Server VLAN  
✓ Users CANNOT access Management or Guest VLANs (blocked)  
✓ Guest can ONLY access Internet (all internal blocked)  
✓ pfSense logs show blocked connection attempts  

![Management](Images/FWTest-MGMT1.png)  
![Management](Images/FWTest-MGMT2.png)  
*Successful Management Firewall Verification*  
![User](Images/FWTest-USER.png)  
*Successful User Firewall Verification*
![Guest](Images/FWTest-GUEST.png)  
*Successful Guest Firewall Verification*
![Server](Images/FWTest-SERVER.png)  
*Successful Server Firewall Verification*

**📁ACTIVE DIRECTORY TESTS**  
✓ Domain join successful for Windows 10 workstations  
✓ Domain users can log in to workstations  
✓ Computer objects appear in correct OUs  
✓ DNS integrated with AD (SRV records present)  
✓ Domain replication status: Healthy (dcdiag passed) 

![Domain Join Success](Images/ComputerName.png)  
*homelab.local domain computer name*
![Domain Login](Images/LoginScreen.png)  
*Login screen showing HOMELAB domain*
![Whoami Output](Images/Whoami.png)  
*whoami command showing HOMELAB\username*
![Domain Controller Validation](Images/Nltest.png)  
*nltest /dsgetdc showing DC01 as domain controller*  

**👨‍🔧SERVICE ACCESS TESTS**    
✓ IIS website accessible from Management and Users VLANs  
✓ IIS website blocked from Guest VLAN (firewall working)  
✓ File share accessible: \\DC01\Shared  
✓ NTFS permissions enforced (access denied for unauthorized folders)  
✓ Mapped drive (S:) appears automatically after GPO  

![Web Access - Management VLAN](Images/Web-MGMT.png)  
*Accessing IIS website from Management VLAN*
![Web Access - Users VLAN](Images/Web-USER.png)  
*Accessing IIS website from Users VLAN*
![Web Access - Guest Blocked](Images/Web-GUEST.png)  
*Cannot access IIS website from Guest VLAN (blocked by firewall)*  

**👥GROUP POLICY TESTS**  
✓ Desktop wallpaper applied after gpupdate  
✓ Network drive mapping automated (S: drive)  
✓ Desktop shortcuts created for IT Staff OU  
✓ GPO inheritance working correctly  

![Desktop Wallpaper Applied](Images/GPOWallpaper.png)  
*Desktop wallpaper automatically applied via GPO*
![Auto-Mapped Drive](Images/GPOAutoMapped.png)  
*S: drive automatically mapped on user login*

**🛡️SECURITY VALIDATION**  
✓ Guest VLAN completely isolated from internal networks  
✓ Users cannot access Management VLAN (security boundary)  
✓ File access controlled by AD group membership  
✓ NTFS permissions more restrictive than share permissions  
✓ Default deny firewall policy (only allowed traffic passes)  

![Server Manager - Roles](Images/ServerRoles.png)  
*Server Manager showing all installed roles on DC01*

## 🚨TROUBLESHOOTING PERFORMED

**⚠️ISSUES ENCOUNTERED & RESOLUTIONS**

Issue: VM not getting DHCP address
Resolution: 
- Verified VirtualBox network adapter attached to correct Internal Network
- Checked pfSense DHCP service status (Services > DHCP Server)
- Used ipconfig /release and /renew to refresh
- Confirmed firewall rules allow DHCP (UDP 67/68)

Issue: Cannot ping between VLANs
Resolution:
- Reviewed firewall rules on each interface
- Verified rule order (blocks before allows)
- Checked pfSense firewall logs to see dropped packets
- Applied correct rules and tested again

Issue: DNS not resolving domain names
Resolution:
- Verified DNS server set to 192.168.40.10 (DC01)
- Checked DC01 DNS service is running
- Verified DNS forwarders configured (8.8.8.8)
- Flushed DNS cache: ipconfig /flushdns

Issue: Cannot access file share
Resolution:
- Confirmed share permissions include user's group
- Verified NTFS permissions (more restrictive)
- Used net use command to troubleshoot: net use * \\DC01\Shared
- Checked user is member of appropriate security group in AD

Issue: Group Policy not applying
Resolution:
- Ran gpupdate /force on client
- Verified GPO linked to correct OU
- Checked GPO not disabled
- Reviewed Event Viewer for Group Policy errors
- Used gpresult /r to confirm applied policies

## SKILLS DEMONSTRATED

**🛜NETWORKING**  
✓ VLAN configuration and segmentation    
✓ Subnetting and IP addressing schemes (CIDR notation)  
✓ Routing configuration (inter-VLAN routing)  
✓ DHCP server configuration   
✓ DNS configuration and troubleshooting  
✓ NAT configuration for internet access  
✓ Network troubleshooting (ping, tracert, ipconfig, nslookup)  

**🛡️SECURITY**  
✓ Firewall rule creation and management  
✓ Network segmentation for security zones  
✓ Access Control Lists (ACLs)  
✓ Principle of least privilege implementation  
✓ NTFS permission configuration  
✓ Share-level permissions  
✓ Group-based access control  
✓ Security testing and validation  

**🪟WINDOWS SERVER ADMINISTRATION**  
✓ Windows Server 2022 installation and configuration  
✓ Active Directory Domain Services deployment  
✓ Domain Controller promotion  
✓ Organizational Unit design and implementation  
✓ User and group management  
✓ Computer object management  
✓ DNS server administration (integrated with AD)  
✓ IIS web server installation and configuration  
✓ File server configuration  
✓ Print server setup  

**👨‍👨‍👦‍👦GROUP POLICY**  
✓ GPO creation and linking  
✓ User configuration policies  
✓ Computer configuration policies  
✓ Group Policy Preferences (drive mapping, shortcuts)  
✓ GPO scope and inheritance  
✓ Policy troubleshooting (gpupdate, gpresult)  

**👾VIRTUALIZATION**  
✓ VirtualBox configuration and management  
✓ Virtual machine creation and resource allocation  
✓ Virtual networking (Internal Networks, NAT)  
✓ Snapshot management  
✓ VM performance tuning  

**📝DOCUMENTATION**  
✓ Network topology documentation  
✓ Configuration documentation  
✓ Troubleshooting logs  
✓ Testing and validation records  
✓ Technical writing  

## 🧠CONCLUSION
This home lab successfully demonstrates a comprehensive understanding
of enterprise IT infrastructure including networking, security, Windows
Server administration, and Active Directory. The project showcases
practical skills that are directly transferable to professional IT
environments.

Key achievements:
- Designed and implemented secure, segmented network
- Deployed and configured Windows Server with AD DS
- Implemented group-based access control
- Automated configuration with Group Policy
- Validated security controls through testing

This lab serves as a foundation for continued learning and can be
expanded with additional services, security implementations, and
advanced configurations.

*Project completed: December 31, 2025*  
*Documentation version: 1.0*
