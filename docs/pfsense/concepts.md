---
title: Basic Concepts
layout: default
parent: pfSense
nav_order: 1
---
# Concepts to Understand

## Network Interface Cards (NICs)
For a pfSense firewall setup, you need at least three network interfaces:

- **WAN Interface:** The connection between the firewall and the internet or external network.
- **LAN Interface:** The internal network that pfSense will protect.
- **Management Interface:** A dedicated interface for configuring pfSense through its web GUI.

Each of these interfaces is connected to a physical or virtual network adapter, and the firewall uses these interfaces to manage traffic based on your defined rules.

## Virtualization with VirtualBox
In this setup, we will use **VirtualBox** to create virtual machines (VMs) for both pfSense and Ubuntu. VirtualBox is a free and open-source hypervisor that allows you to run multiple operating systems on a single host machine. We'll be configuring virtual NICs in VirtualBox to represent the various network interfaces needed by pfSense.

## VLANs (Virtual Local Area Networks)
A **VLAN** is a network segment that operates independently of physical hardware. It allows you to logically group devices, regardless of their physical location, for better traffic management and security. VLANs are identified by a VLAN ID (ranging from 1 to 4095). The key benefit of VLANs is the ability to separate traffic between different groups, ensuring better isolation and reducing broadcast traffic.

## Switches and Tagged VLANs
A **Layer 3 (L3) Switch** operates at both the data link layer (Layer 2) and the network layer (Layer 3). Unlike a Layer 2 switch, which only forwards data based on MAC addresses, an L3 switch can also route traffic between different VLANs using IP addresses. This makes it a powerful solution for inter-VLAN communication within a network.

### Handling VLANs and Tagged Traffic  
When working with VLANs, an L3 switch must be configured to manage **tagged traffic**. Tagged traffic refers to Ethernet frames that contain a VLAN ID, which helps the switch determine which VLAN the traffic belongs to. The switch then processes the traffic based on VLAN configurations and routing rules:

1. **Intra-VLAN Traffic (Switching):** If traffic is destined for another device within the same VLAN, the L3 switch forwards it at Layer 2 using MAC addresses, just like an L2 switch.
2. **Inter-VLAN Traffic (Routing):** If traffic needs to move between different VLANs, the L3 switch routes it at Layer 3 based on IP addresses.

### Trunk Ports and Tagged VLANs  
- **Trunk Ports:** These are switch ports that carry traffic for multiple VLANs. They use **802.1Q VLAN tagging**, where each Ethernet frame is marked with a VLAN ID to differentiate traffic.
- **Access Ports:** These are switch ports assigned to a single VLAN, meaning they only send and receive untagged traffic for that VLAN.

By leveraging VLAN tagging and built-in routing capabilities, an L3 switch allows efficient network segmentation and optimized traffic flow between VLANs without requiring an external router.

## Input and Output Ports on Switches
Switches have multiple **input and output ports**. When a tagged VLAN packet is received on an input port, the switch uses the VLAN ID to decide which output ports should forward the packet. Each port can be assigned to a specific VLAN, effectively isolating traffic for different groups of users or devices.
