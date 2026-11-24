# Port Security and SSH

## 1. Objective
Apply basic switch-port security and secure remote management.

## 2. Port Security
Document the access ports protected, maximum allowed MAC addresses, violation action, and whether sticky MAC learning was used.

## 3. SSH Configuration
Document the devices configured for SSH, management IP addresses, SSH version, and authentication method. Do not publish passwords or private keys.

## 4. Configuration
Insert the actual port-security and SSH commands used.

Example verification commands:

```cisco
show port-security
show port-security interface [INTERFACE]
show ip ssh
show running-config
```

## 5. Testing Results
Record whether unauthorized devices were restricted as expected and whether SSH management access worked.

## 6. Screenshots
Add port-security status and SSH connection screenshots. Hide usernames or sensitive information if necessary.
