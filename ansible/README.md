# First of all
* Replace it with your own password and user.
* I turned off the Gather_facts module for all tasks to save resources.
```
---
- name: Configure ssh Connection
  hosts: node
  gather_facts: false
  connection: local
  vars_files: #Define server password
    - vars/server.yml
  tasks:
    - name: configure ssh connection
      shell: |
        ssh-keyscan {{inventory_hostname}} >>~/.ssh/known_hosts
        sshpass -p'{{server_password}}' ssh-copy-id yourNon-rootUser@{{inventory_hostname}}
```
* Install ansible and confirm the existence of the ansible-playbook and ansible-galaxy commands
* Guide through official documents  https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
```
 #If it is centos  
 yum install ansible
 ```

* Configure host groups and non-root user in the hosts file in the ansible configuration file directory (usually in /etc/ansible/hosts). I use Node as a group and a non-root user as ansible_user.
```
#This is my configuration
[node]
192.168.1.1

[node:vars]
ansible_user=lighthouse
```

# Install the service templates using Ansible-Galaxy 
```
ansible-galaxy install geerlingguy.docker
ansible-galaxy install geerlingguy.mysql
```

# Then use ansible-playbook to execute them sequentially
```
ansible-playbook initServer.yaml
ansible-playbook initMysql.yaml
ansible-playbook docker-main.yaml
ansible-playbook nginx-main.yml
ansible-playbook bak-mysql.yml  

# About the backup
* Scenario 1: Use crontab to back up data on the server.
* In scenario 2, pull the backup locally via playBook.
* In solution 3, upload the backup file to the cloud platform based on Solution 1.
* Usually, multiple backup schemes are required to ensure reliable backup. This is just an example of a local server backup.

# About Test
* I have a Tencent Cloud server that can reload the system unlimited times to test the reliability of Ansible-Playbook. In practice, I would do the same with the actual test (using the same system environment as the customer) to ensure the reliability of the results.
* Test YAML syntax
```
ansible-playbook --syntax-check nginx-main.yml
```
