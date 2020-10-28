## 1. Potential problems with playbooks

The playbook is great because we can add multiple plays and tasks into one playbook to control and configure different operating systems. This is convenient because everything is stored in one file. 

However, when we have a large system with a lot of devices at different departments, The approach "putting everything in one file" may create a problem because the playbook will be very long and complex.

Ansible came up with a new approach which can solve this problem. Ansible lets users organize tasks in a directory structure called a **Role**.

