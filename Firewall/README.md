## Overview
Fortinet FortiGate virtual firewall used to secure WAN-LAN traffic, manage DMZ, and implement port forwarding.

## Purpose
- Filter and inspect incoming/outgoing traffic.
- Protect web server in DMZ.
- Control LAN-to-WAN and WAN-to-LAN access.

## Configuration Flow
1. Assign IP to LAN port (Port2) for Web GUI access
2. Configure WAN port (Port1) to connect to external network
3. Create firewall policies for LAN/WAN/DMZ
4. Enable application layer inspection (e.g., block SSH on WAN)
5. Configure port forwarding for web server
6. Test DMZ accessibility from WAN

## NOTE
This is a free version of FortiGate NGFW for virtual machine. This only works with 1 vCPU and 2 GB memory. 
You need to register yourself to FortiCloud by creating an account and then login using same account in Virtual Machine to register it. One Machine per account. 