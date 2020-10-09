
## 1. Introduction
* An Ansible ad-hoc command uses the /usr/bin/ansible command-line tool to automate a single task on one or more managed nodes. 
* It is quick and easy, and it is great for tasks we repeat rarely such as rebooting all the machines or shutting down all the machines. Instead of writing a playbook, I can run a quick ad-hoc command. 
* Sometimes, we can test a specific task by using an ad-hoc command before committing it to a playbook. 
**Syntax**
ansible [pattern] -m [module] -a "[module options]"
* pattern: the managed host(s)
* module: the Ansible module we intend to use
* module options: arguments

## 2. Woorking with routers

Example:
I will pull some information from the routers in the network.

First, I create a host list for the management routers and the backbone router.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/12.png)

The interfaces on the managementRT list:

**Note**:
* -u: Username
* -k: Password

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/13.png)

The interfaces on the backboneRT list:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/14.png)

Also, I can check the status of Hot Standby Router Protocol on both management routers:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/15.png)

I can choose to run the command against two inventories:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/16.png)

I can also extract the output to a file:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/17.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/18.png)

**Note:**
I use the module **raw** in this case because this module doesn't require Python installed on the remote system, and routers don't have Python installed on the system.

## 3. Working with CentOS:

#### Module file:

This module is used to set attributes of files and directories. Also, we use it to remove files and directories.

* To create a file and set its permissions:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/19.png)

Checking back on the machine: (the list vlan40 contains 3 machines, but I will show only the results from the first machine as examples.)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/20.png)

* To change permissions of a file:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/21.png)

Checking back on the machine:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/22.png)

* To change the owner and the group of the file:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/23.png)

Checking back on the machine:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/24.png)

* To create a directory:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/25.png)

Checking back on the machine:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/26.png)

* To delete a directory recursively:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/27.png)

Checking back on the machine:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/28.png)

#### Module yum:

We use the module yum to install, upgrade, uninstall, and list packages.

* To install a package, specify the state **installed**

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/29.png)

**Note:** 
* To ensure the latest version is installed, use the state **latest**
* To remove a package, use the state **absent** or **remove**

Checking back on the machine:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/30.png)
