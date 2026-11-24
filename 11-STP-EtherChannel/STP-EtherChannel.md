# STP and EtherChannel

## 1. Objective
Document Layer 2 loop prevention and link aggregation between switches.

## 2. STP Configuration
Record the STP mode, root bridge, and any priority settings configured.

## 3. EtherChannel Configuration
| Port-channel | Connected switches | Member interfaces | Protocol |
|---|---|---|---|
| [Port-channel] | [Switches] | [Interfaces] | [LACP / PAgP / Static] |

## 4. Configuration
Insert the actual STP and EtherChannel commands used.

Example verification commands:

```cisco
show spanning-tree
show etherchannel summary
show interfaces port-channel [NUMBER]
```

## 5. Testing Results
Record the STP root bridge and whether EtherChannel formed successfully. If tested, document behavior after a member link was disconnected.

## 6. Screenshots
Add STP status and EtherChannel summary screenshots.
