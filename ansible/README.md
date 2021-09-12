# First of all
* You need to configure the non-root user on the target server and enter the password in the first task of the initServer.yaml file. Then use the public key to log in directly.
* I turned off the Gather_facts module for all tasks to save resources.
```
---
- name: Configure ssh Connection
  hosts: node
  gather_facts: false
  tasks:
    - name: configure ssh connection
      shell: |
        ssh-keyscan {{inventory_hostname}} >>~/.ssh/known_hosts
        sshpass -p'yourpassword' ssh-copy-id yourNon-rootUser@{{inventory_hostname}}
```
* Install ansible and confirm the existence of the ansible-playbook and ansible-galaxy commands
* Guide through official documents  https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
```
 #If it is centos  
 yum install ansible
 ```

* Configure host groups and non-root user in the hosts file in the ansible configuration file directory (usually in /etc/ansible/hosts). I use Node as a group and a non-root user as remote_user.

# Install the service using Ansible-Galaxy 
```
ansible-galaxy install geerlingguy.docker
ansible-galaxy install geerlingguy.mysql
```

# Then use ansible-palyBook to execute them sequentially
```
ansible-playbook initServer.yaml
ansible-playbook initMysql.yaml
ansible-playbook docker-main.yaml
ansible-playbook nginx-main.yml
ansible-playbook bak-mysql.yml  #You need to create a new database first, otherwise the backup list is empty.
```

# About the backup
* Scenario 1: Use crontab to back up data on the server.
* In scenario 2, pull the backup locally via playBook.
* In solution 3, upload the backup file to the cloud platform based on Solution 1.
* Usually, multiple backup schemes are required to ensure reliable backup. This is just an example of a local server backup.

# About Test
* I have a Tencent Cloud server that can reload the system unlimited times to test the reliability of Ansible-Playbook. In practice, I would do the same with the actual test (using the same system environment as the customer) to ensure the reliability of the results.
