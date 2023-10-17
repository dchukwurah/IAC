# What is Ansible?

Ansible is an open-source automation tool that automates software provisioning, configuration management, and application deployment. It helps in managing servers, configuring operating systems, orchestrating containers, and deploying applications seamlessly.

## Uses of Ansible

- **Configuration Management**: Managing configurations of systems, ensuring that systems are in the desired state.

- **Provisioning**: Setting up multiple servers in the infrastructure.

- **Application Deployment**: Automating the deployment of applications

- **Continuous Delivery**: Ansible helps in setting up a Continuous Delivery (CD) pipeline, ensuring that code changes are automatically deployed to the production environment.

- **Security Automation**: Automating applying security patches/compliance with security policies.

- **Orchestration**: It allows you to run tasks in sequence or parallel, coordinating the tasks between different servers, and managing complex deployments.


## Steps to install and connect on ansible

### 1. **Launch an EC2 Instance:**

   - Choose the 'Ubuntu' Amazon Machine Image (AMI) - ami-0136ddddd07f0584f .
   - Configure security group  and allow necessary ports such as **SSH** and **HTTP**
   - Configure the other aspects of the AMI in the same way the app was set up or DB to allow mongo if setting up DB too
   - Review and launch the instance.

### 2. **Access the EC2 Instance:**

   - Connect to the EC2 instance using SSH.
     ```bash
     ssh -i "<name of pem file>.pem" ec2-user@your-ec2-public-ip
     ```

### 3. **Update the agent (EC2 Instance) and set up ansible:**

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

### 5. **Configuration and Inventory Setup:**

   - Create or modify the Ansible configuration file 

### 6. **SSH Key Pair Setup:**

For identification 
Open a gitbash terminal and cd into the .ssh folder and copy over the pem file into the instance 
Using the SCP command, type `scp -i "~/.ssh/tech254.pem" ~/.ssh/tech254.pem ubuntu@<instance public DNS IP>:~/.ssh` (change to include the IP of the instance)

### Note:
- Check you have successfully copied the files by going to the .ssh files and ls 
- Chmod 400 file to ensure you can run it in the respective instance
- Ensure that the EC2 instances you aim to manage with Ansible have SSH and other necessary ports open.
- Adjust the security groups and network ACLs as necessary to allow connectivity between the Ansible controller and the target hosts.

# Connecting ansible:

1. Cd into the Ansible directory `cd /etc/ansible`
2. Open hosts file in nano in order to configure the host nodes.
`sudo nano hosts`
3. Configure permitted hosts in the file by adding the instances:

```
[web]
ec2-instance ansible_host=<public_ip> ansible_user=ubuntu ansible_ss_private_key_file=/home/ubuntu/.ssh/file.pem

```

4. Ping to ensure there is a secure connection

`sudo ansible web -m ping` 

```
ec2-instance | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

6. Now we are securely connected we can directly run commands and get information about the hosts from the controller
 For example `sudo ansible web -a "uname -a"` will return information about the operating system being used.