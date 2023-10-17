## Why Use YAML Files for Playbooks?

### Readability

- YAML stands for "YAML Ain't Markup Language". It is human-friendly and very easy to understand. YAML files use indentation and basic symbols to represent the hierarchy and structure of the data, making it readable.

### Simplicity

- YAML files are simple to write and understand. They avoid the use of quotes and braces, which makes them less cluttered and more straightforward compared to JSON or XML.

### Structure

- YAML files can naturally represent data structures like lists and dictionaries, making them suitable for Ansible playbooks where these structures are common.

### Integration

- Ansible integrates seamlessly with YAML. Playbooks, which are the cornerstone of Ansible's configuration, deployment, and orchestration functionalities, are written in YAML format.

### Standardization

- Using YAML files for playbooks helps in maintaining a standard format, which can be understood and used consistently by different team members and tools.


#### Ansible, with its simplicity and powerful capabilities, helps in automating various IT tasks, and the use of YAML files for playbooks makes the process more manageable and standardized.



#### We need to learn yaml because its very popular and Ansible and Docker use Yaml

# Creating a yaml file to do configuration management/provisioning

We want a script that will go and install ngnix and node without us having to go in manually
## We can create a yaml file in the default location
# To create a playbook to provision nginx web server in web-node
---
# yaml files starts with three dashes

# where do you want to install or run this playbook?
- hosts: web

# find the facts (see the logs) - optional
  gather_facts: yes

# provide admin access(permissions) to this playbook
  become: true

# provide the actual instructions - install nginx
  tasks:
  - name: provision/install/configure Nginx
    apt: pkg=nginx state=present
# we need to ensure nginx is running/ enable







sudo ansible-playbook <name of the playbook/file/yamlfile


1. Start by creating a YAML file for our App instance provision file:

```
sudo nano install-nginx.yml
```

2. Create a "playbook" to provision nginx web server in the web node:

```
# Create a playbook to provision nginx web server in the web node
---
# starts with three dashes.

# where do you want to install or run this playbook?
- hosts: web


# find the facts (see the logs) - optional
  gather_facts: yes


# provide admin access to this playbook - use sudo
  become: true


# provide the actual instructions - install nginx
  tasks:
  - name: provision/install/configure Nginx
    apt: pkg=nginx state=present


# ensure nginx is running/enabled
```

NOTE: YAML files traditionally (although no longer required) start with the three dashes at the top: "---". This is no longer needed, but can still be used.

# Ansible Usage:

We have now created our Ansible playbook for installing and running nginx. Let's now remotely run this in the app instance:

```
ansible-playbook install-nginx.yml
```

If it successful, we should see the following:

```
PLAY [web] ********************************************************************************************************************************************************************************************************

TASK [Gathering Facts] ********************************************************************************************************************************************************************************************
ok: [ec2-instance]

TASK [provision/install/configure Nginx] **************************************************************************************************************************************************************************
changed: [ec2-instance]

PLAY RECAP ********************************************************************************************************************************************************************************************************
ec2-instance               : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
