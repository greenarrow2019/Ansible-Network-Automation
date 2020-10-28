## 1. Introduction

Sometimes, when we want to execute a task or tasks with Ansible multiple times, we can write an ad-hoc command, but that command may be long and hard to remember.

There is a better way which is to save the task(s) into a playbook and run the playbook when we want to execute the task(s). For example, when we add a new machine to the system, we can run the playbook to push out new configurations and confirm those new configurations instead of writing many ad-hoc commands. 

## 2. Syntax

A playbook is written in YAML language which is human-readable.

A playbook consists of one or more **plays** in an ordered list which means Ansible will execute each play at a time from top
to bottom. each **play** contains one or more **tasks**, and each **task** calls an Ansible module. If a play has more than one task, 
Ansible will also run each task from top to bottom one at a time against all machines matched by the host pattern. 

Each play or each task usually has a **name** attribute, and Ansible will display the **name** of the play or the task after it is run. When Ansible finishes executing all the play(s), it provides a summary of the targeted machines and how they perform. 

## 3. Examples

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/32.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/31.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/33.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/36.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/34.png)

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/35.png)

