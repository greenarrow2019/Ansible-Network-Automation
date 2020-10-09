
## 1. Introduction
* An Ansible ad-hoc command uses the /usr/bin/ansible command-line tool to automate a single task on one or more managed nodes. 
* It is quick and easy, and it is great for tasks we repeat rarely such as rebooting all the machines or shutting down all the machines. Instead of writing a playbook, I can run a quick ad-hoc command. 
* Sometimes, we can test a specific task by using an ad-hoc command before committing it to a playbook. 

**Syntax**
ansible [pattern] -m [module] -a "[module options]"
* pattern: the managed host(s)
* module: the Ansible module we intend to use
* module options: arguments

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
