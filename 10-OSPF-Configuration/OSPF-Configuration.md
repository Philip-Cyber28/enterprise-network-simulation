# OSPF Configuration

## 1. Objective

The objective of this task is to implement Open Shortest Path First (OSPF) routing to dynamically exchange routing information between participating Layer 3 devices.

OSPF allows routers to automatically learn remote network routes without requiring manual static route configuration. This enables communication between different VLANs and remote networks.

The main objective is to establish OSPF neighbor relationships between the participating devices and verify connectivity by testing communication from R1 to R3 using the ping command.

## 2. Implementation

OSPF is configured on the participating Layer 3 devices to advertise their directly connected networks.

The network topology includes the following connections:

- ISP to R1: 10.0.0.0/30
- R1 to R2: 10.0.0.4/30
- R2 to Core Switch: 10.0.0.8/30

The internal network consists of the following VLANs:

| VLAN | Department | Network | Default Gateway |
|---|---|---|---|
| 10 | SERVER | 192.168.10.0/24 | 192.168.10.1 |
| 20 | IT | 192.168.20.0/24 | 192.168.20.1 |
| 30 | HR | 192.168.30.0/24 | 192.168.30.1 |
| 40 | ADMIN | 192.168.40.0/24 | 192.168.40.1 |
| 50 | FINANCE | 192.168.50.0/24 | 192.168.50.1 |
| 60 | SALES | 192.168.60.0/24 | 192.168.60.1 |
| 70 | MANAGEMENT | 192.168.70.0/24 | 192.168.70.1 |
| 80 | GUEST | 192.168.80.0/24 | 192.168.80.1 |

The server network contains the following servers:

| Server | IP Address | Default Gateway |
|---|---|---|
| WEB | 192.168.10.10 | 192.168.10.1 |
| DNS | 192.168.10.20 | 192.168.10.1 |
| DHCP | 192.168.10.30 | 192.168.10.1 |

OSPF allows participating devices to exchange routing information dynamically and provides routes to remote networks.

## 3. OSPF Details

| Device | Process ID | Area | Networks advertised |
|---|---|---|---|
| R1 | 10 | Actual area | 10.0.0.4/30 |
| R2 | 10 | Actual area | 10.0.0.4/30, 10.0.0.8/30 |
| Core Switch | 10 | Actual area | 10.0.0.8/30 and configured VLAN networks |

## 4. Configuration

OSPF is configured using Cisco IOS commands. The following commands demonstrate the configuration syntax using process ID 1 and area 0 as examples.

**R1 Configuration:**

    enable
    configure terminal
    router ospf 10
     network 10.0.0.4 0.0.0.3 area 0
    end
    write memory

**R2 Configuration:**

    enable
    configure terminal
    router ospf 10
     network 10.0.0.4 0.0.0.3 area 0
     network 10.0.0.8 0.0.0.3 area 0
    end
    write memory

**Core Switch Configuration:**

    enable
    configure terminal
    router ospf 10
     network 10.0.0.8 0.0.0.3 area 0
     network 192.168.10.0 0.0.0.255 area 0
     network 192.168.20.0 0.0.0.255 area 0
     network 192.168.30.0 0.0.0.255 area 0
     network 192.168.40.0 0.0.0.255 area 0
     network 192.168.50.0 0.0.0.255 area 0
     network 192.168.60.0 0.0.0.255 area 0
     network 192.168.70.0 0.0.0.255 area 0
     network 192.168.80.0 0.0.0.255 area 0
    end
    write memory

These are example configurations. The actual process ID, area, and network statements must match the implemented network topology.

## 5. Verification

After configuring OSPF, the following commands are used to verify the configuration and routing information on each participating device.

**Check OSPF Neighbors:**

    show ip ospf neighbor

This command displays neighboring OSPF routers and their adjacency states. A FULL state indicates that the OSPF adjacency has been successfully established.

**Check Routing Protocols:**

    show ip protocols

This command displays the active routing protocols, OSPF process information, and advertised networks.

**Check OSPF Routes:**

    show ip route ospf

This command displays routes learned dynamically through OSPF. OSPF routes are identified by the letter O in the routing table.

**Check OSPF Interfaces:**

    show ip ospf interface brief

This command displays the interfaces participating in OSPF and their associated areas.

**Test Connectivity from R1 to R3:**

    ping [R3-IP-ADDRESS]

Replace [R3-IP-ADDRESS] with the actual IP address of R3.

A successful ping indicates that IP connectivity exists between R1 and R3 through the network.

## 6. Testing Results

OSPF verification is performed to confirm that the participating Layer 3 devices establish neighbor relationships and exchange routing information successfully.

The following tests are used to evaluate the implementation:

| Test | Expected Result |
|---|---|
| OSPF Neighbor Verification | Neighbor relationships reach the FULL state |
| Routing Protocol Verification | OSPF process and network information are displayed |
| OSPF Routing Table | Remote OSPF routes appear with the O code |
| OSPF Interface Verification | Correct interfaces and areas are displayed |
| R1 to R3 Ping Test | Successful ICMP replies are received |

The final connectivity test is performed by sending ICMP packets from R1 to R3.

If the ping test is successful, it confirms that a working network path exists between the two devices. If the test fails, the IP addressing, interface status, OSPF neighbor relationships, routing tables, and return path should be checked.

Actual testing results should be recorded based on the commands executed on the network devices.

## 7. Screenshots

The following screenshots provide evidence of the OSPF configuration and verification.

**R1 to R3 Connectivity Test**

This screenshot shows the ping test performed from R1 to R3 to verify end-to-end connectivity.

![R1 to R3 Ping Test](/Screenshots/ospf-r1-to-r3-ping.png)
