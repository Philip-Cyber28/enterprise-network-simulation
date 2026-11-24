
# STP and EtherChannel

## 1. Objective

Document Layer 2 loop prevention and link aggregation between switches using Spanning Tree Protocol (STP) and EtherChannel.

The main objectives are:
- Prevent Layer 2 switching loops using STP.
- Configure EtherChannel between switches.
- Verify link aggregation and redundancy.
- Configure trunk links to carry VLAN traffic.
- Configure PortFast and BPDU Guard.

---

## 2. STP Configuration

Spanning Tree Protocol (STP) prevents Layer 2 switching loops and maintains a loop-free network topology.

The configuration includes:
- Spanning-tree configuration.
- Root bridge verification.
- PortFast configuration.
- BPDU Guard configuration.
- Spanning-tree status verification.

### 2.1 STP Configuration Details

| Parameter | Details |
|---|---|
| STP mode | To be confirmed |
| Root bridge | To be confirmed |
| Bridge priority | To be confirmed |
| PortFast | Configured on AS1 |
| BPDU Guard | Configured on AS1 |

### 2.2 STP Screenshots

- `Screenshots/spanning-tree-cs`
- `Screenshots/spanning-tree-as1`
- `Screenshots/portfast-as1`
- `Screenshots/bpdu-guard-as1`

---

## 3. EtherChannel Configuration

EtherChannel combines multiple physical links into one logical connection between switches, providing increased bandwidth and redundancy.

### 3.1 EtherChannel Devices

| Switch | Configuration |
|---|---|
| AS1 | EtherChannel configured and verified |
| AS2 | EtherChannel configured and verified |
| AS3 | EtherChannel configured and verified |

### 3.2 Port-channel Information

| Port-channel | Connected switches | Member interfaces | Protocol |
|---|---|---|---|
| To be confirmed | AS1, AS2, AS3 | To be confirmed | To be confirmed |

### 3.3 EtherChannel Screenshots

**AS1**
- `Screenshots/creating-ether-as1`
- `Screenshots/creating-ether-cs-as1`
- `Screenshots/verify-ether-as1`

**AS2**
- `Screenshots/creating-ether-as2`
- `Screenshots/creating-ether-cs-as2`
- `Screenshots/verify-ether-as2`

**AS3**
- `Screenshots/creating-ether-as3`
- `Screenshots/creating-ether-cs-as3`
- `Screenshots/verify-ether-as3`

**Additional Verification**
- `Screenshots/verify-ether-cs`

---

## 4. Configuration

### 4.1 STP Verification Commands

```cisco
show spanning-tree
show spanning-tree summary
```

### 4.2 EtherChannel Verification Commands

```cisco
show etherchannel summary
show interfaces port-channel 1
```

### 4.3 Trunking Verification Commands

```cisco
show interfaces trunk
```

### 4.4 VLAN Verification Commands

```cisco
show vlan brief
```

### 4.5 Configuration Evidence

The supplied screenshots document:
- EtherChannel configuration on AS1, AS2, and AS3.
- Trunk configuration and verification.
- VLAN creation and verification.
- Spanning-tree configuration.
- PortFast configuration.
- BPDU Guard configuration.

---

## 5. Testing Results

| Test | Result |
|---|---|
| STP configuration | Screenshot evidence provided |
| Root bridge verification | Screenshot evidence provided |
| EtherChannel configuration on AS1 | Screenshot evidence provided |
| EtherChannel configuration on AS2 | Screenshot evidence provided |
| EtherChannel configuration on AS3 | Screenshot evidence provided |
| EtherChannel verification | Screenshot evidence provided |
| Trunking verification | Screenshot evidence provided |
| VLAN verification | Screenshot evidence provided |
| PortFast configuration | Screenshot evidence provided |
| BPDU Guard configuration | Screenshot evidence provided |
| Member link failure test | Not confirmed |

### 5.1 STP Testing

STP configuration and verification screenshots are provided.

Use the following command to verify the root bridge:

```cisco
show spanning-tree
```

### 5.2 EtherChannel Testing

EtherChannel configuration and verification evidence is provided for AS1, AS2, and AS3.

Use the following command to check EtherChannel status:

```cisco
show etherchannel summary
```

### 5.3 Link Failure Testing

A member-link disconnection test should be performed to verify that EtherChannel continues operating when one physical link fails.

Record the results after testing:
- Was the EtherChannel still operational?
- Did traffic continue through the remaining member links?
- Was the failed interface removed from the active bundle?

---

## 6. Trunking and VLAN Screenshots

### 6.1 Trunking Configuration

**AS1**
- `Screenshots/trunking-as1`
- `Screenshots/verify-trunking-as1`

**AS2**
- `Screenshots/trunking-as2`
- `Screenshots/verify-trunking-as2`

**AS3**
- `Screenshots/trunking-as3`
- `Screenshots/verify-trunking-as3`

### 6.2 VLAN Configuration

- `Screenshots/creating-vlan-cs`
- `Screenshots/sh-vlan-creation-cs`

---

## 7. Conclusion

STP and EtherChannel are important components of Layer 2 network infrastructure.

STP prevents switching loops and maintains a stable network topology by controlling redundant paths between switches.

EtherChannel combines multiple physical connections into a single logical link to provide increased bandwidth and redundancy.

The supplied screenshots document the configuration and verification of EtherChannel, trunking, VLANs, spanning tree, PortFast, and BPDU Guard.

These configurations help improve network reliability, availability, and performance.
