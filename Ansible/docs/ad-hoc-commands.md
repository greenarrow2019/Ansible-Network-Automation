
## 1. Introduction
* An Ansible ad-hoc command uses the /usr/bin/ansible command-line tool to automate a single task on one or more managed nodes. 
* It is quick and easy, and it is great for tasks we repeat rarely such as rebooting all the machines or shutting down all the machines. Instead of writing a playbook, I can run a quick ad-hoc command. 
* Sometimes, we can test a specific task by using an ad-hoc command before committing it to a playbook. 

**Syntax**
ansible [pattern] -m [module] -a "[module options]"
* pattern: the managed host(s)
* module: the Ansible module we intend to use
* module options: the options of that module

