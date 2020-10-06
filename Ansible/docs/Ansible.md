## 1. Why do we need Ansible?
In the past, system administrators had to manage servers and routers by hand such as installing software manually, changing configuration one by one, and managing them individually.  

However, as businesses started growing bigger, a big business would likely have more users, more servers, and more network divices. This created a huge issue because it would take a lot of time to configure and manage all those devices, and businesses weren't happy to pay more money to get more people to do the same task over and over again. 

The need for network automation grew, and Ansible is one of the best network automation tool on the market. 

For example, a business has 10 routers and two servers. They can log in to each of them via SSH to make changes then log out. With Ansible, if they want the same configuration for 10 routers, Ansible will log in to 10 devices at the same time via SSH and push the configuration out to them. This will save a lot of time comparing to configure each of them manually. 

## 2. What is Ansible?
Ansible is an automation and configuration management technology used to provision, deploy, and manage compute infrastructure across cloud, virtual, and physical environments. 

Ansible is an open source automation platform, but it also has a paid version called **Ansible Tower**. 

Ansible aims for simplicity and easy to understand while maintaining the efficiency. Also, it is a popular tool because it doesn't require client machines to install a client application for this to work. Ansible can be installed on a control machine, which then uses SSH by default to communicate with the managed machines.

**Control node requirements**
* Currently Ansible can be run from any machine with Python 2 or Python 3 installed. This includes Red Hat, Debian, CentOS, macOS, and so on. Windows is not supported for the control node. 
* When choosing a control node, it is recommended to put the control machine near the machines being managed. 
**Managed node requirement**
* SSH is up and running properly. 

## 3. Basic Concepts
* Control node
  * Any machine with Ansible installed.
  * We can have multiple control nodes.
  * The configuration file is located at /etc/ansible/ansible.cfg
* Managed nodes
  * The network devices andd/or servers we manage with Ansible.
  * Ansible doesn't need to be installed on managed nodes.
* Inventory
  * A list of managed nodes. 
  * Managed nodes can be assigned into different groups for better management. 
  * The default inventory file is at **/etc/ansible/hosts**
  * You can use the **-i option** to specify the inventory file if you don't use the default inventory file. 
* Modules
  * The units of code Ansible executes.
  * Each module has a particular use.
* Tasks
  * The units of action in Ansible.
* Playbooks
  * Ordered lists of tasks, saved so we can run those tasks in that order repeatedly. 
  * Playbooks are written in YAML.
## 4. Installing Ansible
I will install Ansible on CentOS 8 machine in VLAN50.
* To install Ansible for CentOS 8, first ensure that the CentOS 8 EPEL (Extra Packages for Enterprise Linux) repository is installed:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/4.png)

* Once the repository is installed, install Ansible with **yum**:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/1.png)

* Checking the version of Ansible to make sure it is installed:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/2.png)

* Testing it by pinging the localhost:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/3.png)

* Next, generating a new SSH key on the control node:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/5.png)

* Because the control node connects to the managed nodes via SSH, I copy the newly generated SSH public key from the control node to the managed nodes:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/6.png)

* Creating a host list in the **hosts** file:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/8.png)

* pinging the managed machines:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/7.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/9.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/11.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/10.png)

We can see how Ansible can help me save time because I can ping multiple machines at the same time. 

