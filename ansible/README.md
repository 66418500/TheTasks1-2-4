# First of all
* You need to configure the non-root user on the server and enter the password in the first task of the initserver. yaml file. Then use the public key to log in directly.

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
