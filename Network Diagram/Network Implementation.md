I built a network diagram and configured every node manually before using Ansible for automation because I wanted to make sure every command worked when I typed them.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/1.png)

For every router and switch, I configured a hostname, a secret password, and a local account. Also, I set up the console port, the auxiliary port, and the VTY ports (Telnet and SSH) to use the local account's credential to log in. In addition, because all passwords configured on an IOS (Internetwork Operating System) device, with the exception of the passwords configured with **enable secret password**, are stored in clear-text in the device configuration file. To encrypt all the passwords, I used the command **service password-encryption* in global configuration mode.

Also, I shut down all the ports that I didn't use on the routers and switches. For every working port on each router, I gave it an IP address as shown in the network diagram. There is one exception which is port GigabitEthetnet0/0 on the router BackboneRT because it received an IP address from the modem in the house.

## Linux14 - Gateway to the Internet

I set up **Port Address Translation** on Linux14 and used it as a gateway to the Internet because I wasn't eble to bypass captive portal from BackboneRT.

## BackboneRT
To let all the machines inside the network to access the Internet, I enabled **Port Address Translation** on this router. Port G0/2 has an **inside global** address, and ports G0/0, G0/1, and G0/3 each has an **inside local** address. 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/4.png)

## ManagementRT1 and ManagementRT2
On both routers, I enabled **Hot Standby Router Protocol (HSRP)** to provide redundancy for the local subnets. This protocol allows me to configure one router as the active router and the other router as the standby router. All the routers in a single HSRP group shares a single virtual MAC address and a virtual IP address, which acts as a default gateway for the local network. The **active router** is responsible for forwarding the traffic, and the **standby router** will take up the responsibility of the **active router** and forwards the traffic if the **active router** fails. 

The process of choosing the active router and the standby router is automatic, but I set them up manually for this lab. ManagementRT1 is the active router for VLAN 10, VLAN 30, and VLAN 50. ManagementRT2 is the active router for VLAN 20 and VLAN 40. I can manipulate this process by setting up the active router to have a higher priority than the standby router. Also, to make sure that the active router for each VLAN will always be that router if the active router fails and comes back up later, I used the command **standby preempt** which will enable the HSRP router with the highest priority to immediately become the active router. 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/2.png)
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/3.png)

**NOTE:**

In addition, because routers don't forward broadcast packets, machines in VLAN 10, 20, and 30 won't receive IP addresses from the DHCP server in VLAN 40 because they aren't in the same physical subnet. To solve this problem, I enabled relay agents on both routers on interfaces g0/0, g0/1, and g0/2.

Because I set up two management routers for redundancy, when a client machine sends a DHCP Discover message, it will be flushed to both routers which means the DHCP server will receive two DHCP Discover messages from one machine. In a large network, this can create unnecessary traffic. The solution is to only allow the active HSRP router to forward this message. 

First, I gave each HSRP group a name.

Second, I used the command **ip helper-address 192.168.50.12 to let only the active router for that VLAN to forward the DHCP Discover messages to the DHCP server.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/16.png)
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/17.png)
 
## SyslogSW, GuestSW, StudentSW, TeacherSW, AdminSW, and OfficeSW

There are six VLANs in the network:
* VLAN 10: Guest VLAN
* VLAN 20: Student VLAN
* VLAN 30: Teacher VLAN
* VLAN 40: Admin VLAN
* VLAN 50: Syslog VLAN
* VLAN 60: Office VLAN

eigrpRT will provide IP addresses to client machines in VLAN 60. Also, machines in VLAN 40 and VLAN 50 all have static IP addresses.

The DHCP server in VLAN 40 will provide IP addresses to the machines in VLAN 10, VLAN 20, VLAN 30.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/10.png)

The spannning tree protocol mode in these switches is **Rapid Per-VLAN Spanning Tree Plus.** (RPST+)
**Note**: I wanted to implement a two-tier LAN network to show how RPST+ worked in a network, but I wasn't able to get an EVE image for Switch Layer 3.

On theses switches, for each edge port, I enabled **PortFast** and **BPDUguard**. 

**PortFast** will cause a switch port to enter the spanning tree forwarding state immediately, bypassing the learning state. This feature helps client machines to receive IP addresses from a DHCP server immediately when they boot up and don't have to wait for the spanning tree protocol to finish converging. 

Also, the edge ports are the ports that connect to client machines so that they don't typically transmit or receive **Bridge Protocol Data Units** (BPDUs). However, someone may plug a switch into one of these edge ports to learn about the network or to alter the network. To prevent that from happening, I enabled **BPDU guard** on these edge ports. If an edge port receives a BPDU, the switch will move that port into an errdisable state.

In addition, I enabled **port security** with options **violation restrict, maximum 1, and mac-address sticky** on all the edge ports so that each edge port only accepts the first MAC address it receives. If a different machine is plugged in, the switch will receive an alert about it. 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/11.png)

## eigrpRT

I also enabled **Port Address Translation** on this router with G0/0 as the **inside global** port and G0/1 as the **inside local** port.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/14.png)


## Routing Protocols
* OSPF area 0: BackboneRT, ManagementRT1, and ManagementRT2.
    * On BackboneRT, I used the command **ip route 0.0.0.0 0.0.0.0 G0/2** to to route all traffic to the Internet and added it to the routing table by using the command **default-information originate**.  
    
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/12.png)

* OSPF area 1: the link betweek BackboneRT and RedistributeRT.
* EIGRP: RidistributeRT and EIGRP router.

On RedistributeRT, to enable OSPF and EIGRP to work together, I used router redistribution so that EIGRP routes will appear as OSPF routes in OSPF routers' routing tables and vice versa. 
**Note:** Router redistribution helps increase accessibility within networks.

**ManagementRT1**

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/5.png)

**ManagementRT2**

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/6.png)

**BackboneRT**

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/7.png)

**RedistributeRT**

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/8.png)

**eigrpRT**

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/9.png)

To make sure that route redsitribution worked, I browsed to the Internet from machine Linux26 in Office VLAN.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Network%20Diagram/Images/15.png)


