### ***Index***

[1. Introducing EVE-NG](#1)
[2. Installing EVE-NG](#2)
- [2.1. Prepare](#2.1)
- [2.2. Installation and Configuration](#2.2)
-- [1. Open the EVE ova file](#2.2.1)
-- [2. Browse to the directory containing the downloaded EVE ova file and _Open_ it](#2.2.2)
- [2.3. Make sure the storage path is correct and click _Import_](#2.3)
- [2.4. After importing the virtual machine successfully, click _Edit virtual machine settings_ and edit as follow.](#2.4)
- [2.5. When the VM is booted for the first time, the screen will ask users to log in with the username _root_ and the password _eve_.](#2.5)
- [2.6. Enter a new password for user _root_](#2.6)
- [2.7. Type the hostname](#2.7)
- [2.8. Type the DNS domain name](#2.8)
- [2.9. Set up an IP address for the VM](#2.9)
- [2.10. Type a NTP server if used](#2.10)
- [2.11. Choose direct connection](#2.11)
[3. Complete the installation and access the user interface via a browser](#3)
[4. Configure Wireshark](#4)

---

<a name = '1'></a>
# 1. **Introducing EVE-NG**

UNetLab, or the Unified Networking Lab, is a virtual lab for networking engineers who want to explore and learn networking concepts or test networking designs. It is a Web-based competitor to options such as GNS3 and Cisco VIRL. UNetLab can be seen as a hypervisor for images that typically run on physical network devices or internal separate virtual machines.

The great thing about UNetLab (and EVE-NG) is that everything is contained in a virtual machine, and users use a web interface to create and manage labs.

EVE-NG (Emulated Virtual Environment - Next Generation) is the successor to UnetLab which contains more powerful features compared to UnetLab. EVE-NG is a graphical network emulator that supports both commercial and open-source router images. Its graphical user interface runs in a web browser. Users may create network nodes from a library of templates, connect them together, and configure them.

<a name = '2'></a>
# 2. **Installing EVE-NG**
There are two ways to install EVE-NG on Vmware Workstation:
- Download the EVE ova file and open it directly.
- Download the iso file and set it up.

The ova and iso files can be downloaded [here](https://www.eve-ng.net/index.php/download/).

For this project, I will install and configure EVE-NG on Vmware WorkStation using the EVE ova file which contains the EVE-NG image that was pre-installed. If users want to install EVE-NG using the iso file, instruction can be found [here](https://www.youtube.com/watch?v=Kxt5dvuAfNk).
<a name = '2.1'></a>
## 2.1. **Prepare**
Required installation packages:
    - The EVE-NG ova file
    - The bundled Telnet, VNC, rpc packages for Windows environment can be downloaded [here](https://www.eve-ng.net/index.php/download/).
    - Vmware Workstation.
    
<a name = '2.2'></a>
## 2.2. **Installation and Configuration**
After downloading the necessary software, open Vmware Workstation and do the following steps:
<a name = '2.2.1'></a>
#### 1. Open the EVE ova file 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/1.png)
<a name = '2.2.2'></a>
#### 2. Browse to the directory containing the downloaded EVE ova file and _Open_ it
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/2.png)

<a name = '2.3'></a>
## 2.3. Make sure the storage path is correct and click _Import_        
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/3.png)

<a name = '2.4'></a>
## 2.4. After importing the virtual machine successfully, click _Edit virtual machine settings_ and edit as follow. Two boxes in the virtualization engine section need to be checked.
    
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/4.png)

<a name = '2.5'></a>
## 2.5. When the VM is booted for the first time, the screen will ask users to log in with the username _root_ and the password _eve_. 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/5.png)

<a name = '2.6'></a>
## 2.6. Enter a new password for user _root_   
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/6.png) 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/7.png)

<a name = '2.7'></a>
## 2.7. Type the hostname
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/8.png)

<a name = '2.8'></a>
## 2.8. Type the DNS domain name 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/9.png)

<a name = '2.9'></a>
## 2.9. Set up an IP address for the VM. For this project, I configure a static address for convenience.                     
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/10.png)          
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/11.png) 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/12.png) 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/13.png) 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/14.png) 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/15.png)
<a name = '2.10'></a>
## 2.10. Type a NTP server if used 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/16.png)
<a name = '2.11'></a>
## 2.11. Choose direct connection 
![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/17.png)

<a name = '3'></a>
# 3. **Complete the installation and access the user interface via a browser**

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/18.png)

The default credential for the web interface:
- Username: admin
- Password: eve

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/19.png)

Install the Windows client-side package

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/20.png)

<a name = '4'></a>
# 4. **Configure Wireshark**

To use Wireshark to capture packets on devices in EVE-NG environment, I need to configure the _wireshark\_wrapper.bat_ file using notepad running as administrator and type the password in.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/21.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/images/22.png)
