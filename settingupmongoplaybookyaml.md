# we need to set up a playbook to installm mongo into our ec2 instance
# everything will happen in the ansible controller


# this playbook is to set up mongodb in the ec2
---
# agent node name/ip

- hosts: db

# gather facts(logs)
  gather_facts: yes

# provide admin access
  become:true

# provide instructions
  tasks:
  - name: set up mongodb in db ec2
    apt: pkg=mongodb state=present

# ensure db is in a running state

