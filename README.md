
# MOHTECH Solutions | Enterprise Network Infrastructure

**A redundant enterprise network designed and implemented using Cisco technologies in EVE-NG.**

This project builds on the MOHTECH Solutions company scenario introduced in a previous project. It focuses on designing and implementing an enterprise network infrastructure for the organization in a simulated EVE-NG environment.

The project demonstrates practical networking concepts including network segmentation, gateway redundancy, dynamic routing, and Internet connectivity.

---

## Network Topology

![MOHTECH Network Topology](Moh-top.png)

---

## Technical Overview

| Category | Implementation |
|---|---|
| Environment | EVE-NG |
| Network Devices | 1 Router, 2 Distribution Switches, 2 Access Switches |
| Network Design | Two-Tier Campus Architecture |
| Routing Protocol | OSPF |
| Gateway Redundancy | HSRP |
| Loop Prevention | PVST |
| Link Aggregation | EtherChannel (LACP) |
| IP Allocation | DHCP |
| External Connectivity | NAT/PAT |

## Network Architecture

The internal switching infrastructure follows a **two-tier campus architecture**, consisting of a Distribution Layer and an Access Layer.

| Tier | Devices | Main Responsibilities |
|---|---|---|
| Distribution | DSW1, DSW2 | Inter-VLAN routing, HSRP, OSPF, spanning-tree |
| Access | ASW1, ASW2 | End-device connectivity and VLAN assignment |

R1 operates as the edge router, providing upstream connectivity between the internal network and the ISP.

## VLAN & IP Addressing

Four VLANs were created to separate the organization's departments and management traffic.

| VLAN | Department | Network | HSRP Virtual Gateway |
|---|---|---|---|
| 10 | IT | 10.10.10.0/24 | 10.10.10.254 |
| 20 | Sales | 10.10.20.0/24 | 10.10.20.254 |
| 30 | HR | 10.10.30.0/24 | 10.10.30.254 |
| 90 | Management | 10.10.90.0/24 | 10.10.90.254 |

## Key Technologies

| Technology | Implementation |
|---|---|
| VLANs | Departmental network segmentation |
| Inter-VLAN Routing | Communication between VLANs |
| HSRP | Redundant default gateways |
| PVST | Layer 2 loop prevention |
| EtherChannel | Aggregated links between distribution switches using LACP |
| OSPF | Dynamic routing between distribution switches and edge router |
| DHCP | Automatic IP address allocation |
| NAT/PAT | Internet access for internal networks |

### Redundancy Design

Gateway responsibilities are distributed across the two distribution switches:

- **DSW1:** Active gateway for VLANs 10 and 20.
- **DSW2:** Active gateway for VLANs 30 and 90.

The HSRP virtual gateway addresses use the `.254` address in each VLAN subnet.

Spanning-tree root bridge placement is aligned with the HSRP active gateway roles to help optimize Layer 2 forwarding paths.

## Implementation Workflow

The network was built in the following stages:

1. **Topology Design** – Planned the network architecture, devices, links, VLANs, and IP addressing.
2. **Switching Configuration** – Created VLANs, configured access ports and trunks, and implemented EtherChannel.
3. **Layer 3 Configuration** – Configured inter-VLAN routing and HSRP on the distribution switches.
4. **Routing** – Implemented OSPF between the distribution layer and edge router.
5. **Network Services** – Configured DHCP on R1 and NAT/PAT for external connectivity.
6. **Verification** – Tested address allocation, connectivity, and Internet access.

## Connectivity & DHCP Verification

The following screenshot demonstrates successful DHCP address allocation and connectivity testing from the network hosts.

![DHCP Leases and Successful Ping Tests](Leases.png)

- **DHCP:** Hosts successfully obtained IP addresses from the DHCP server running on R1.
- **Connectivity:** Successful ping tests confirmed network reachability from the hosts.

## Device Configurations

- [R1 Configuration](R1.txt)
- [DSW1 Configuration](DSW1.txt)
- [DSW2 Configuration](DSW2.txt)
- [ASW1 Configuration](ASW1.txt)
- [ASW2 Configuration](ASW2.txt)

## Network Documentation

- [Network Documentation & IP Addressing Plan](MohTechSolutions_Network_Documentation-v8.xlsx)

## EVE-NG Lab

- [Download EVE-NG Lab Export](%5FExports_unetlab_export-20261122-185541.zip)

The exported lab is provided for anyone who wants to explore the topology and configurations. Compatible device images are required to run the lab.

---

**Focus Areas:** Enterprise Networking · Routing & Switching · Network Redundancy · Cisco IOS · EVE-NG
