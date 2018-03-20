# ansible-vagrant-lb-web
POC for HA website using Ansible, Vagrant, Nginx and Apache

- Ansible version : ansible 2.4.3.0

- Vagrant Version : 2.0.3

Implementation of a website using Nginx as a load balancer, and N Apache web servers behined the load balancer.

Vagrant : build and configure the virtual servers on Ubuntu 16.4 boxes.

Ansible : provision the servers.

## Run

1. git clone https://github.com/mabozkika/ansible-vagrant-lb-web.git

2. cd ansible-vagrant-lb-web

3. vagrant up


## Test 

- Type the load balancer ip (10.10.10.11) on your browser.

- Refresh the page multiple times to see each node data.


## Destroy all the servers

- vagrant destroy -f

