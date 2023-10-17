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

### We want a script that will go and install ngnix and node without us having to go in manually
### We can create a yaml file in the default location

```
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
 ```
To run the playbook we can run the command
```
sudo ansible-playbook <name of the playbook/file/yamlfile
```
e.g. 
```
ansible-playbook install-nginx.yml
```
We can now do the same for node.js
```
# To create a playbook to provision nodejs version 12 in web-node
---
# yaml files starts with three dashes

# where do you want to install or run this playbook?
- hosts: web

# find the facts (see the logs) - optional
  gather_facts: yes

# provide admin access(permissions) to this playbook
  become: true

# provide the actual instructions - install nodejs version 12
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Node.js dependencies
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - curl
        - software-properties-common

    - name: Install the gpg key for nodejs LTS
      apt_key:
       url: "https://deb.nodesource.com/gpgkey/nodesource.gpg.key"
       state: present

    - name: Add NodeSource repository
      apt_repository:
        repo: "deb https://deb.nodesource.com/node_12.x {{ ansible_distribution_release }} main"
        state: present
        update_cache: yes
        filename: nodesource

    - name: Install Node.js
      apt:
        name: nodejs
        state: present

```
