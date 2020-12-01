### ***Table of contents***

[1. Defining variables](#1)

[2. BackboneRT](#2)

[3. ManagementRT1](#3)

[4. ManagementRT2](#4)

[5. Confirmation](#5)

---

<a name = '1'></a>
## 1. Defining variables

For this project, I decided to set up the same username and password for management router 1, management router 2, and the backbone router. 

* Management Router 1:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/37.png)

* Management Router 2:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/38.png)

* Management Backbone Router:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/39.png)

**Connection variables**

Connection variables are normally used to set the specifics on how to execute actions on a target.

* ansible_connection: define the connection plugin.

When I use the connection plugin **network_cli**, I need to specify the **network_os** variable for the specific network platform I am communicating with.

* ansible_network_os: specify the operating system of the targeted host.

**Note**: each platform uses different connection type. 

[Platform Options](https://docs.ansible.com/ansible/latest/network/user_guide/platform_index.html#platform-options)

For Cisco IOS platform, it uses **network_cli** as the **ansible_connection** and **ios** as the **network_os**.

* ansible_user: the user Ansible will log in as.

* ansible_password: the password of the user Ansible uses to log in as.

The Cisco IOS platform supports privilege escalation, where certain tasks must be done by a privileged user. 
On Cisco routers, this is called the **enable** mode.

* ansible_become and ansible_become_method enables Ansible to run a task or playbook with escalated privileges. 

* ansible_become_password: this password will enable privilege mode. 

<a name = '2'></a>
## 2. BackboneRT

When Ansible runs this playbook for backbone router, it will look for those variables that were defined in the **hosts** file under **backboneRT:vars**.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/42.png)

When the playbook is run successfully, the **failed count** equals 0.

I created a playbook to configure the following:
|  |  |
| --- | --- |
|  Setting up the hostname  |  Update the login banner  |  
|  Remove the motd banner  |  Remove the exec banner  |
|  Enable password encryption and disable ip domain-lookup  |
|  Console password  |  Auxiliary port password  |
|  Loopback  |  G0/0  |
|  G0/1  |  G0/2  |
|  G0/3  |  OSPF  |
|  Static route to the Internet  |  acl for PAT  |
|  configure PAT  |  save the configuration  |

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/43.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/44.png)

<a name = '3'></a>
## 3. ManagementRT1

When Ansible runs this playbook for management router 1, it will look for those variables that were defined in the **hosts** file under **managementRT1:vars**.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/41.png)

When the playbook is run successfully, the **failed count** equals 0.

I created a playbook to configure the following:
|  |  |
| --- | --- |
|  Setting up the hostname  |  Update the login banner  |  
|  Remove the motd banner  |  Remove the exec banner  |
|  Enable password encryption and disable ip domain-lookup  |
|  Console password  |  Auxiliary port password  |
|  Loopback  |  G0/0  |
|  G0/1  |  G0/2  |
|  G0/3  |  G0/4  |
|  G0/5  |  shutdown unused ports  |
|  OSPF  |  save the configuration  |

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/45.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/46.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/47.png)

<a name = '4'></a>
## 4. ManagementRT2

When Ansible runs this playbook for management router 2, it will look for those variables that were defined in the **hosts** file under **managementRT2:vars**.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/40.png)

When the playbook is run successfully, the **failed count** equals 0.

I created a playbook to configure the following:
|  |  |
| --- | --- |
|  Setting up the hostname  |  Update the login banner  |  
|  Remove the motd banner  |  Remove the exec banner  |
|  Enable password encryption and disable ip domain-lookup  |
|  Console password  |  Auxiliary port password  |
|  Loopback  |  G0/0  |
|  G0/1  |  G0/2  |
|  G0/3  |  G0/4  |
|  G0/5  |  shutdown unused ports  |
|  OSPF  |  save the configuration  |

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/48.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/49.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/50.png)

<a name = '5'></a>
## 5. Confirmation

To confirm that those playbooks were applied successfully to the targeted routers, I also wrote three playbooks that would print out **running-config** from those routers.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/51.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/52.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/53.png)

* **register** is being used in these files to save the response of the command **show running-config** into the "print_output** variable.

* The **debug** mode is used to print the contents of **print_output**

I ran the **showBackbone.yml** file to check the configuration on the Backbone Router.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/54.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/55.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/56.png)

