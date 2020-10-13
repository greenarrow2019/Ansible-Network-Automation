### ***Table of contents***

[1. Introducing EVE-NG](#1)

[2. Installing EVE-NG](#2)

[3. Completing the installation and accessing the user interface](#3)

[4. Configuring Wireshark](#4)

---

<a name = '1'></a>
# 1. Introducing EVE-NG

UNetLab, or the Unified Networking Lab, is a virtual lab for networking engineers who want to explore and learn networking concepts or test networking designs. It is a Web-based competitor to options such as GNS3 and Cisco VIRL. UNetLab can be seen as a hypervisor for images that typically run on physical network devices or internal separate virtual machines.

The great thing about UNetLab (and EVE-NG) is that everything is contained in a virtual machine, and users use a web interface to create and manage labs.

EVE-NG (Emulated Virtual Environment - Next Generation) is the successor to UnetLab which contains more powerful features compared to UnetLab. EVE-NG is a graphical network emulator that supports both commercial and open-source router images. Its graphical user interface runs in a web browser. Users may create network nodes from a library of templates, connect them together, and configure them.

<a name = '2'></a>
# 2. Installing EVE-NG
There are two ways to install EVE-NG on Vmware Workstation:

- Download the EVE ova file and open it directly.

- Download the iso file and set it up.

The ova and iso files can be downloaded [here](https://www.eve-ng.net/index.php/download/).

For this project, I will install and configure EVE-NG on Vmware WorkStation using the EVE ova file which contains the EVE-NG image that was pre-installed. If users want to install EVE-NG using the iso file, instruction can be found [here](https://www.youtube.com/watch?v=Kxt5dvuAfNk).

### Preparation
Required installation packages:
- The EVE-NG ova file
    
- The bundled Telnet, VNC, rpc packages for Windows environment can be downloaded [here](https://www.eve-ng.net/index.php/download/).
    
- Vmware Workstation.
    
### Installation and Configuration

After downloading the necessary software, open Vmware Workstation and do the following steps:

#### Open the EVE ova file

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/1.png)

#### Browse to the directory containing the downloaded EVE ova file and _Open_ it

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/2.png)

### Make sure the storage path is correct and click _Import_      

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/3.png)

### After importing the virtual machine successfully, click _Edit virtual machine settings_ and edit as follow. Two boxes in the virtualization engine section need to be checked.
    
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/4.png)

### When the VM is booted for the first time, the screen will ask users to log in with the username _root_ and the password _eve_. 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/5.png)

### Enter a new password for user _root_   

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/6.png) 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/7.png)

### Type the hostname

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/8.png)

### Type the DNS domain name 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/9.png)

### Set up an IP address for the VM. For this project, I configure a static address for convenience.       

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/10.png)          

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/11.png) 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/12.png) 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/13.png) 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/14.png) 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/15.png)

### Type a NTP server if used 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/16.png)

### Direct connection 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/17.png)

<a name = '3'></a>
# 3. Completing the installation and access the user interface via a browser

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/18.png)

The default credential for the web interface:
- Username: admin
- Password: eve

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/19.png)

Install the Windows client-side package

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/20.png)

<a name = '4'></a>
# 4. Configuring Wireshark

To use Wireshark to capture packets on devices in EVE-NG environment, I need to configure the _wireshark\_wrapper.bat_ file using notepad running as administrator and type the password in.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/21.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/22.png)
