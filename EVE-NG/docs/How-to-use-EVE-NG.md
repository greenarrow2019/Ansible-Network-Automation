### ***Table of contents***

[1. Supported Images](#1)

[2. Explaining some concepts](#2)

[3. Directories for images storage](#3)

[4. Accessing EVE-NG](#4)

- [4.1. Installing WinSCP](#4.1)

- [4.2. Adding Cisco IOU to EVE-NG](#4.2)

- [4.3. Adding QEMU images](#4.3)

- [4.4. Adding Linux image pack to EVE-NG VM](#4.4)

- [4.5. Adding Cisco ASAv](#4.5)

[5. Adding Cisco ASAv](5)

---

<a name = '1'></a>
## 1. Supported Images

EVE-NG does not provide images of network devices on their website. Users need to find images of the software simulating the devices in the network model that the EVE-NG supports. You can check out the current images supported by EVE-NG [here](https://www.eve-ng.net/index.php/documentation/supported-images/)

<a name = '2'></a>
## 2. **Explaining some concepts**

- **Dynamips** is an emulator computer program that was written to emulate Cisco routers. It can emulate the hardware of the Cisco series routing platforms by directly booting an actual Cisco IOS software image into the emulator.

- **IOL** or **IOS on Linux** is a Cisco internal way of running IOS on Linux. The IOL images are used to create layer 2 devices (switches) or layer 3 devices (routers) which can help people to practice with the same features and functions that the original devices have. It is not CPU and memory resource intensive which makes it a good choice.

- **qemu** is an open-source emulator and virtualizer that can perform hardware virtualization. 

<a name = '3'></a>
## 3. **Directories for images storage**

- Device images are saved in this directory _/opt/unetlab/addons/_

- In _/opt/unetlab/addons/_ contains 3 folders for three diffrent types of images:
    - dynamips: this folder containing image files used to simulate the IOS of actual network devices such as switches and routers. 
    - iol: this folder contains bin files simulating the IOS operating systems of Cisco network devices.
    - qemu: this folder contains the templates used to create virtual machines to emulate terminal devices such as computers, laptops, and phones.
    
<a name = '4'></a>
## 4. Accessing EVE-NG

I used PUTTY to ssh to the EVE-NG virtual machine for a bigger screen. when I logged in for the first time, I ran _apt-get update && apt-get upgrade_ to update the list of available packages and install the latest versions of all the packages the VM has.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/23.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/24.png)

<a name = '4.1'></a>
#### 1. Installing WinSCP

I used WinSCP to copy file between my local computer and the EVE-NG virtual machine.
Click [here](https://winscp.net/eng/index.php) to download WinSCP.
After installing WinSCP, open a connection the EVE-NG virtual machine.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/25.png)

<a name = '4.2'></a>
#### 2. Adding Cisco IOU to EVE-NG

**Note**: IOL images must end with the ".bin" extension and must be executable. License file must be stored under the same path.
- Transferring the bin files from my local computer to the directory /opt/unetlab/addons/iol/bin on EVE-NG VM.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/26.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/27.png)

- Check the folder to make sure the files are there.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/28.png)

**Note**: 
    - **iourc** is the license file.
    - **L3-ADVENTERPRISEK9-M-15.2-M5.3.bin**: This one is for Router
    - **L2-ADVENTERPRISEK9-M-15.2-20150703.bin**: This one is for Switch Layer 2
    - **L2-ADVENTERPRISEK9-M-15.2-IRON-20151103.bin**: This one is for Switch Layer 3
- Finally, to make sure the permissions have been set correctly, EVE-NG provides a script to fix any permission issues. This script is recommended to run every time a new image is added to the EVE-NG virtual machine.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/29.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/30.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/31.png)

- After importing the IOL image files of Cisco devices into EVE-NG virtual machine, go to the web interface and add some new nodes to make sure they work.
- Creating a new project:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/32.png)

- On the left side, click _Add an object_ then click _Node_:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/33.png)

- The Cisco IOL line is blue which means it's ready to be used.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/34.png)

- When setting the parameters for the node, I can choose one of the images I imported and an appropriate icon for the node.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/35.png)

<a name = '4.3'></a>
#### 3.Adding QEMU images

**Note**: The naming of the images in qemu is a bit different from iol. The rules are listed [here](https://www.eve-ng.net/index.php/documentation/qemu-image-namings/)
- Transferring the images for layer 2 switch and router to the correct folder.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/36.png)

**Note**: Remember to run this script to fix permissions after uploading an image.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/37.png)

- In the browser, add a new node to check if both layer 2 switch and router are ready to use.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/38.png)

- The Cisco vIOS Router and Cisco vIOS switch lines are blue which mean they are ready for use.

<a name = '4.4'></a>
#### 4. Adding Linux image pack to EVE-NG VM

EVE-NG lets users upload Linux images to the VM, and EVE-NG also provides ready to go and prepared Linux image pack on their [website](https://www.eve-ng.net/index.php/documentation/howtos/howto-create-own-linux-host-image/). For this project, I used the pre-install Linux images they provide.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/39.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/40.png)

Universal credentials in all the Linux images provided by EVE-NG:
- root/root
- root/eve
- user/Test123
- root/Test123
**Note**: If you want to create your own custom Linux host, remember to check the rules for naming.
After that, go to the web interface to make sure they are correctly installed and ready to use.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/41.png)

I can choose the Linux Image I like to use.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/42.png)

<a name = '4.5'></a>
#### 5. Adding Cisco ASAv

- Upload the correct image to the correct folder in _/opt/unetlab/addons/qemu/_

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/43.png)

- Rename the original image name to _virtoia.qcow2_

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/44.png)

- Remember to clean and fix permissions:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/45.png)

- Go to the web interface to check if it's there. The blue line means it's ready.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/EVE-NG/images/46.png)
