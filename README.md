# Ansible playbook to setup shadowsocks server

## Introdution
This repo provides an ansible playbook to setup a shadowsocks server with docker.

For docker installation the [docker role from geerlingguy](https://github.com/geerlingguy/ansible-role-docker) has been used.

## Setup
##### Clone project
`git clone git@github.com:AlirezaDastyar/shadowsocks-ansible.git`

##### Install docker role from ansible galaxy [[Link](https://galaxy.ansible.com/geerlingguy/docker)]
`ansible-galaxy install geerlingguy.docker` 

##### Change the `inventory.ini` parameters 
Replace the `127.0.0.1` with you'r server ip or domain name.
Set the `username` and `password` to appropriate and safe values for shadowsocks user.
```ini
[ss_server]
127.0.0.1 username=ShadowSocksUser password=VerySecurePassowrd
```

#####  Make `.env` file based on template.env
Copy the `docker/template.env` to `docker/.env` and set the right parameters for shadowsocks configs
```properties
METHOD=aes-256-gcm
PASSWORD=VerySecurePassword
PORT=25555
```
##### Run it
Run the following command and provide the root password for ssh

`ansible-playbook setup.yml -i inventory.ini -k`
