Infrastructure as Code (IaC) and Configuration Management & Configuration Management Orchestration are two key concepts in the realm of DevOps, cloud computing, and IT operations. 

The following will detail the important information about the concepts, how they are related and the steps we can take to set up Ansible to be a controller for our EC2 instances. 

### **Infrastructure as Code (IaC):**

   - **Definition**: IaC is a key DevOps practice that involves managing and provisioning computing infrastructure through machine-readable script files, rather than using physical hardware configuration or interactive configuration tools.
   
   - **Components**:
     - **Code Files**: Script files are written using languages like YAML, JSON, or domain-specific languages such as Terraform.
     - **Version Control**: These script files are often kept in version control systems like Git, allowing for tracking changes, collaboration, and rollback if necessary.
     
   - **Benefits**:
     - **Automate the Deployment**: Speed up the infrastructure deployment process.
     - **Consistency**: Ensure the infrastructure is deployed consistently and reliably.
     - **Scalability**: Easier to scale the infrastructure as per requirements.
     
   - **Use Cases**: 
     - Cloud infrastructure provisioning such as in AWS
     - Network configuration, database configuration, and server configuration.

### **Configuration Management Orchestration**:

   - **Definition**: It refers to the coordination and management of different aspects of an application or system configuration. Orchestration in configuration management involves automating various tasks and workflows to ensure systems are configured correctly and work seamlessly together.
   
   - **Components**:
     - **Automation Tools**: Tools like Ansible, Puppet, and Chef are used for orchestration.
     - **Scripts and Playbooks**: Defines the steps and processes for configuration.
     
   - **Benefits**:
     - **Coordination**: Ensures different parts of the system work together seamlessly.
     - **Automated Workflows**: Automate repetitive tasks to ensure efficiency and accuracy.
     
   - **Use Cases**: 
     - Application deployment.
     - System configuration across multiple machines.
     - Automating workflows and processes.

### Relationship Between IaC and Configuration Management Orchestration:

- **Complementary Practices**: While IaC focuses on provisioning the underlying infrastructure, configuration management orchestration focuses on managing and coordinating the configuration of the systems and applications running on that infrastructure.
  
- **Interlinked Workflows**: In a typical DevOps workflow, IaC can be used to set up the necessary infrastructure, followed by configuration management orchestration to ensure systems and applications are correctly configured and integrated.
  
- **Unified Objective**: Both aim to automate and streamline the processes involved in infrastructure and application management, aiming for speed, reliability, and consistency in deployment and operations.

In conclusion, while IaC and configuration management orchestration may focus on different layers of the technology stack, they are intertwined practices that collectively enhance the automation and manageability of infrastructures and applications in a DevOps environment.

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


Managing infrastructure manually is like manually packaging boxes. Whereas this is like doing this using a machine that automatically packages.


# What is configuration management

This process can be part of an automation pipeline that will speeds up deployment. Ansible is a popular program used to update instances or do other processes within them like changing config files or opening ports, provided the IPs and SSH credentials. This is referred to as  **configuration management**.

# What is orchestration

Orchestration is an aspect of IaC that is on managing and coordinating deployment automatically in multiple different systems at once. 

Essentially configuration management is like one instrument but orchestration can be done on many instances like an orchestra over an entire ASG for example.

# IAC Diagram
![](C:\Users\ChiedozieChukwurah\Repos\IAAC\ansiblescrsh.png)

Our master Node is our local which controls and manages other nodes on the network.
Ansible is our controller which we access via SSH to manage the control the others . 
Ansible connects to both the app and DB instances via SSH to do configuration management automatically - Ansible as is agentless.
Ansible uses vault authenticationT access keys for instances are saved in order to securely connect. 
