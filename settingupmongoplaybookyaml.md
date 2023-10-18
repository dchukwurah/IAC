## Playbook for MongoDB Configuration

#### Ansible needs to be able to do all of our configuration management - not necessarily launch things, as a devops engineer we need to know when to automate and when not to.
#### We need to be able to set up a playbook to install mongo into our ec2 instance, everything will happen through the ansible controller
#### Our playbook should be able to migrate, backup and configure data.


# this playbook is to set up mongodb in the ec2
```yaml
# agent node name/ip
- hosts: db

# gather facts(logs)
  gather_facts: yes

# provide admin access
  become: true

# provide instructions
  tasks:
  - name: set up mongodb in db ec2
    apt: pkg=mongodb state=present

# ensure db is in a running state
```

# this playbook is to set the bindip in mongodb
```yaml
---
# agent node name/ip
- hosts: db

# gather facts(logs)
  gather_facts: yes

# provide admin access
  become: true

# provide instructions
  tasks:
  - name: Stop MongoDB
    ansible.builtin.systemd:
      name: mongodb
      state: stopped
      
  - name: Change bind IP in MongoDB conf
    ansible.builtin.lineinfile:
      path: /etc/mongodb.conf
      regexp: '^  bindIP:127.0.0.1'
      line: ' bindIp: 0.0.0.0'
      backrefs: yes
      
  - name: Restart MongoDB
```

# this playbook is to set the environment variable in the app in mongodb
```yaml

---
# agent node name/ip
- hosts: app

# gather facts(logs)
  gather_facts: yes

# provide admin access
  become: true

# provide instructions
  tasks:
    - name: Add environment variable to ~/.bashrc
      lineinfile:
        path: /home/ubuntu/.bashrc
        line: 'export DB_HOST1=mongodb://52.214.113.152'
```
---
#### Another example
---
 
- hosts: db
  gather_facts: yes
  become: true
 
  tasks:
    - name: set up mongodb in db ec2
      apt: pkg=mongodb state=present
 
    - name: bindip
      lineinfile:
        path: /etc/mongodb.conf
        regexp: '^bind_ip = 127\.0\.0\.1'
        line: 'bind_ip = 0.0.0.0'

# Orchestration with Terraform
