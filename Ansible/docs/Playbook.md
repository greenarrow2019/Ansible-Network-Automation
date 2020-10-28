## 1. Introduction

Sometimes, when we want to execute a task or tasks with Ansible multiple times, we can write an ad-hoc command, but that command may be long and hard to remember.

There is a better way which is to save the task(s) into a playbook and run the playbook when we want to execute the task(s). For example, when we add a new machine to the system, we can run the playbook to push out new configurations and confirm those new configurations instead of writing many ad-hoc commands. 

## 2. Syntax

A playbook is written in YAML language which is human-readable.

**Note**: Indentation is an important part in YAML language.

A playbook consists of one or more **plays** in an ordered list which means Ansible will execute each play at a time from top
to bottom. each **play** contains one or more **tasks**, and each **task** calls an Ansible module. If a play has more than one task, 
Ansible will also run each task from top to bottom one at a time against all machines matched by the host pattern. 

Each play or each task usually has a **name** attribute, and Ansible will display the **name** of the play or the task after it is run. When Ansible finishes executing all the play(s), it provides a summary of the targeted machines and how they perform. 

## 3. Examples

### getarp.yml

This playbook was run against the backboneRT. The purpose of this playbook was to get the arp table from that router.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/32.png)

The image above is an example of a simple playbook written in YAML. 

A YAML file normally has **---** at the beginning of the file to indicate the start of the file.

Then, all the plays will begin at the same indentation level starting with a **- ** (a dash and a space)

#### Some components that may appear in a play:

* name: A description of a play or a task. This is where we can write what the play or the task is about. 

* hosts: a list of devices that is the play's target.

* gather_facts: Normally, Ansible will automatically gather facts about the targeted devices before executing the play(s). In this 
example, I turn off facts gathering by setting the ketword **gather_facts** to **false**.

* tasks: A list of task(s) to be executed in the play. Each task normally starts with a **name** to indicate the start of a task. 

* register: This is the name of variable that will contain task status and module return data.

* debug: this line will print the result out on the screen.

**Note**: Indentation is important in YAML.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/31.png)

When I ran the playbook getarp.yml, it printed out the name of the play, the name of the task, the output of the task, and the summary of the playbook.

### apache.yml

This playbook was run against all the hosts in vlan 30. This playbook was used to install Apache on CentOS.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/33.png)

The targeted hosts were the hosts in vlan 30.

By default, Ansible will run in parallel against all the targeted hosts. However, there is a way to define how many hosts Ansible can run against at a time
using the keyword **serial**. In this example, I told Ansible to run against two machines at a time. By doing this, I could prevent lagging and save bandwidth for other tasks.

Because installing a package is a task for root user, I needed to run this play as root. **remote_user** defines the user used to log into the targeted machines via SSH. 

In this example, I used the **yum** module to install Apache on CentOS. The **name: httpd** specifies the package. The **state: latest** means the latest version of Apache. 

To make sure the service is run on boot, I used the module **service**. The **enabled: true** makes sure Apache starts on boot. The **state: started** indicates the service will start after installing. 

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/36.png)

By default, Ansible doesn't print out facts it gathers from the machines, and it only prints out the result whether the tasks succeed or fail. 

To confirm that Apache was installed successfully on the targeted machines, I went and checked on one of those machines.

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/34.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/35.png)

