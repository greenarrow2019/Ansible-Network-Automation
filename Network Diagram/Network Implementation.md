I built a network diagram and configured every node manually before using Ansible for automation because I wanted to make sure every command worked when I typed them.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/1.png)

For every router and switch, I configured a hostname, a secret password, and a local account. Also, I set up the console port, the auxiliary port, and the VTY ports (Telnet and SSH) to use the local account's credential to log in. In addition, because all passwords configured on an IOS (Internetwork Operating System) device, with the exception of the passwords configured with **enable secret password**, are stored in clear-text in the device configuration file. To encrypt all the passwords, I used the command **service password-encryption* in global configuration mode.

Also, I shut down all the ports that I didn't use on the routers and switches. For every working port on each router, I gave it an IP address as shown in the network diagram. There is one exception which is port GigabitEthetnet0/0 on the router BackboneRT because it received an IP address from the modem in the house.

## BackboneRT
To let all the machines inside the network to access the Internet, I enabled **Port Address Translation** on this router. Port G0/0 has an **inside global** address, and ports G0/1, G0/2, and G0/3 each has an **inside local** address. 

## ManagementRT1 and ManagementRT2
On both routers, I enabled **Hot Standby Router Protocol (HSRP)** to provide redundancy for the local subnets. This protocol allows me to configure one router as the active router and the other router as the standby router. All the routers in a single HSRP group shares a single virtual MAC address and a virtual IP address, which acts as a default gateway for the local network. The **active router** is responsible for forwarding the traffic, and the **standby router** will take up the responsibility of the **active router** and forwards the traffic if the **active router** fails. 

The process of choosing the active router and the standby router is automatic, but I set them up manually for this lab. ManagementRT1 is the active router for VLAN 10, VLAN 30, and VLAN 50. ManagementRT2 is the active router for VLAN 20 and VLAN 40. I can manipulate this process by setting up the active router to have a higher priority than the standby router. Also, to make sure that the active router for each VLAN will always be that router if the active router fails and comes back up later, I used the command ** standby preempt** which will enable the HSRP router with the highest priority to immediately become the active router. 

Also, these two routers will provide an IP address to every machine that belongs to VLAN 50. 

In addition, because routers don't forward broadcast packets, machines in VLAN 10, 20, 30, and 40 won't receive IP addresses from the DHCP server in VLAN 50 because they aren't in the same physical subnet. To solve this problem, I enabled relay agents on both routers with the commmand **ip helper-address 192.168.50.12** on interface e1/0. 

## ManagementSW, GuestSW, StudentSW, TeacherSW, and AdminSW

There are five VLANs in the first network:
* VLAN 10: Guest VLAN
* VLAN 20: Student VLAN
* VLAN 30: Teacher VLAN
* VLAN 40: Admin VLAN
* VLAN 50: Management VLAN

The DHCP server in VLAN 50 will provide IP addresses to the machines in VLAN 10, VLAN 20, VLAN 30, and VLAN 40. Also, the DNS server in VLAN 50 is the DNS server for every machine in VLAN 10, VLAN 20, VLAN 30, VLAN 40, and VLAN 50.

The spannning tree protocol mode in these switches is **Rapid Per-VLAN Spanning Tree Plus.** (RPST+)

On theses switches, for each edge port, I enabled **PortFast** and **BPDUguard**. 
PortFast will cause a switch port to enter the spanning tree forwarding state immediately, bypassing the learning state. This feature helps client machines to receive IP addresses from a DHCP server immediately when they boot up and don't have to wait for the spanning tree protocol to finish converging. 
Also, the edge ports are the ports that connect to client machines so that they don't typically transmit or receive **Bridge Protocol Data Units** (BPDUs). However, someone may plug a switch into one of these edge ports to learn about the network or to alter the network. To prevent that from happening, I enabled **BPDU guard** on these edge ports. If an edge port receives a BPDU, the switch will move that port into an errdisable state.

In addition, I enabled **port security** with options **violation restrict, maximum 1, and mac-address sticky** on all the edge ports so that each edge port only accepts the first MAC address it receives. If a different machine is plugged in, the switch will receive an alert about it. 

Furthermore, DHCP Snooping and Dynamic ARP Inspection were enabled on the switches. 
#### DHCP Snooping
When a machine wants to get an IP address from a DHCP server, it interact with the server through 4 stages:
* DHCP Discover (client)
* DHCP Offer (server)
* DHCP Request (client)
* DHCP ACK (server)

DHCP Snooping is used on a switch to drop DHCP traffic determined to be unacceptable. This feature prevents unauthorized DHCP servers offering IP addresses to DHCP clients. When it is enabled, all switch ports will become **untrusted**, and they will drop all DHCP Offer packets they receive. When we know which port will receive the real DHCP messages, we can configure that port to **trusted** stage, and the DHCP messages won't be dropped.

Because each switch only has one active VLAN, I enabled DHCP Snooping only on the VLAN each switch has with the command **ip dhcp snooping vlan (vlan_ID)** because the feature is inactive on all VLANs.

On GuestSW, StudentSW, TeacherSW, and AdminSW:
* ports G0/0, G0/1, G0/2, and G0/3: untrusted ports.
* ports G1/0 and G1/1: trusted ports.

On ManagementSW:
* ports G1/0, G0/2, and G0/3: untrusted ports.
* ports G0/1:  trusted port.

When the switches receive DHCP ACK messages from the DHCP server, they create a DHCP binding table for record. 

I also configured a rate limit of 20 packets per second on all untrusted ports to prevent **DHCP Starvation Acctack**, and DHCP Snooping will put ports where the rate limit is exceeded into the error-disabled state.

#### Dynamic ARP Inspection (DAI):
Dynamic ARP Inspection only works if DHCP Snooping is enabled on the switches because it uses the DHCP binding table to determine valid IP-to-MAC address.
This feature is used to drop invalid ARP messages which don't have valid IP-to-MAC bindings.
Like DHCP Snooping, when it is enabled, all switch ports will become **unstrusted** and disable on all VLANs.
I put all the ports between switches and routers to **trusted** state.

On GuestSW, StudentSW, TeacherSW, and AdminSW:
* ports G0/0, G0/1, G0/2, and G0/3: untrusted ports.
* ports G1/0 and G1/1: trusted ports.

On ManagementSW:
* ports G1/0, G0/2, and G0/3: untrusted ports.
* ports G0/1:  trusted port.
(to be continued)




**NOTE:**
Because I set up two management routers for redundancy, when a client machine sends a DHCP Discover message, it will be flushed to both routers which means the DHCP server will receive two DHCP Discover messages from one machine. In a large network, this can create unnecessary traffic. The solution is to only allow the active HSRP router to forward this message. 
First, I gave each HSRP group a name.

Second, I used this command in the picture to let only the active router for that VLAN to forward the DHCP Discover messages to the DHCP server.

## Routing Protocols
* OSPF area 0: BackboneRT, ManagementRT1, and ManagementRT2.
    * On BackboneRT, I used the command **ip route 0.0.0.0 0.0.0.0 G0/0** to to route all traffic to the Internet and added it to the routing table by using the command **default-information originate**.  
* OSPF area 1: the link betweek BackboneRT and RedistributeRT.
* EIGRP: RidistributeRT and EIGRP router.

On RedistributeRT, to enable OSPF and EIGRP to work together, I used router redistribution so that EIGRP routes will appear as OSPF routes in OSPF routers' routing tables and vice versa. 
**Note:** Router redistribution helps increase accessibility within networks.

