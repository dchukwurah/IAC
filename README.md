# What is IAAC?


# What is Configuration Management Orchestration

# What is Infrastructure as Code

This is the process of managing and provisioning infrastructure using code.

Managing infrastructure manually is like manually packaging boxes. Whereas this is like doing this using a machine that automatically packages.


# What is configuration management

This process can be part of an automation pipeline that will speeds up deployment. Ansible is a popular program used to update instances or do other processes within them like changing config files or opening ports, provided the IPs and SSH credentials. This is referred to as  **configuration management**.

# What is orchestration

Orchestration is an aspect of IaS that focusses on managing and coordinating deployment automatically in multiple different systems at once. 

Essentially configuration management but can be done on many instances over an entire ASG for example.

# IAAC Diagram
![ansiblescrsh.png](..%2F..%2FDocuments%2FDiagrams%2Fansiblescrsh.png)

1. This is the master node which controls and manages other nodes on the network.
2. Ansible is our controller which we access via SSH. 
3. Ansible connects to instances via SSH to do configuration management automatically Ansible as is agentless.
4. This is the vault contained within Ansible where access keys for instances are saved in order to securely connect. 