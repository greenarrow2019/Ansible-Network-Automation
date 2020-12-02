### ***Table of contents***

[1. Potential problems with playbooks](#1)

[2. Introduction](#2)

---

<a name = '1'></a>
## 1. Potential problems with playbooks

The playbook is great because we can add multiple plays and tasks into one playbook to control and configure different operating systems. This is convenient because everything is stored in one file. 

However, when we have a large system with a lot of devices at different departments, The approach "putting everything in one file" may create a problem because the playbook will be very long and complex.

Ansible came up with a new approach which can solve this problem. Ansible lets users organize tasks in a directory structure called a **Role**. Breaking down a big playbook into multiple small files, and each file only has one purpose can help people work together easily. 

<a name = '2'></a>
## 2. Introduction

An Ansible role has a defined directory structure with seven main standard directories:
* tasks: contains a list of tasks to be executed by the role.
* handlers: contains change handlers by the role. Handlers in this directory can also be used outside of the role.
* files: contains files to be deployed by the role.
* templates: contains templates for the role.
* vars: contains non-default variables for the role.
* defaults: stores default variables for the role.
* meta: defines metadata for the role.

A role doesn't require all seven directories to be present, but a role must have at least one of those directories for it to work.

**Note**: Only create the directories that the role actually uses. 

Also, each included directory must have a **main.yml** file in it because Ansible will look for that file in each available directory when it runs.

An Ansible role normally will have a structure like this:

![](https://github.com/greenarrow2019/Ansible-Network-Automation/blob/master/Ansible/images/57.png)

**Reference**:
[Roles](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html?fbclid=IwAR0-xDxlgcnqAToX7j9pwr1TXrFiFMnsc_ybBncArOSWXLiAZQevO_BCxeU#running-role-dependencies-multiple-times-in-one-playbook)

