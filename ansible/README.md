# First of all
* You need to configure the non-root user on the target server and enter the password in the first task of the initServer.yaml file. Then use the public key to log in directly.
* Install ansible and confirm the existence of the ansible-playbook and ansible-galaxy commands
 ```
 #If it is centos
 yum install ansible
 ```
* Configure host groups and non-root user in the hosts file in the ansible configuration file directory (usually in /etc/ansible/hosts). I use Node as a group

# Install the service using Ansible-Galaxy 
* ansible-galaxy  install geerlingguy.docker
* ansible-galaxy install geerlingguy.mysql

# Then use ansible-palyBook to execute them sequentially
* ansible-playbook initServer.yaml
* ansible-playbook initMysql.yaml
* ansible-playbook docker-main.yaml
* ansible-playbook nginx-main.yml
* ansible-playbook bak-mysql.yml

# About Test
* I have a Tencent Cloud server that can reload the system unlimited times to test the reliability of Ansible-Playbook. In practice, I would do the same with the actual test (using the same system environment as the customer) to ensure the reliability of the results.
