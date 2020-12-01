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

## 2. BackboneRT

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/42.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/43.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/44.png)

## 3. ManagementRT1

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/41.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/45.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/46.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/47.png)

## 4. ManagementRT2

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/40.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/48.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/49.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/50.png)



