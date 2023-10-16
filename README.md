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

# Setting up agent/

1. Connect to your EC2 instance
 
2. Input the following commands...
```
# checks if ansible installed
ansible --version
 
#standard update/upgrade
sudo apt update -y
sudo apt upgrade -y
 
# sets up ansible for install
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
 
# installs ansible
sudo apt update -y
sudo apt install ansible -y
```
 
3. To Copy over the files for identification we need to use the SCP command, Open another git bash and type `scp -i "~/.ssh/tech254.pem" ~/.ssh/tech254.pem ubuntu@<instance public DNS IP>:~/.ssh` (change to include the IP of your instance)
4. Check you have successfully copied the files by going to the .ssh files and ls
5. Chmod 400 file to ensure you can run it in the respective instance