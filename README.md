# Ansible playbook to setup shadowsocks server

## Introduction
This repo provides an ansible playbook to setup a shadowsocks server with docker.

Galaxy roles:
- For docker installation the [docker role from geerlingguy](https://github.com/geerlingguy/ansible-role-docker) has been used.
- For updating packages the [update role from robertdebock](https://github.com/robertdebock/ansible-role-update) has been used.

> [!NOTE]
> Since some VPS(s) are created using old images and contains old packages (i.e ca-certifications) there is a task for updating all system packages if you don't need/want this comment out the update tasks

## Setup
### Clone project
`git clone git@github.com:AlirezaDastyar/shadowsocks-ansible.git`

### Install roles from ansible galaxy [[Link](https://galaxy.ansible.com/geerlingguy/docker)]
`ansible-galaxy install geerlingguy.docker robertdebock.update` 

### Change the `inventory.ini` parameters 
Replace the `127.0.0.1` with you'r server ip or domain name.
Set the `username` and `password` to appropriate and safe values for shadowsocks user.
```ini
[ss_server]
127.0.0.1 username=ShadowSocksUser password=VerySecurePassword
```

###  Config shadowsocks config through `config.json`
I recommend to leave `server` and `server_port` in `config.json` as is.


```json
{
    "server": "0.0.0.0",
    "server_port": 8388,
    "password": "MySecurePassword",
    "method": "aes-256-gcm"
}
```
Also note that the port here is not published port for shadowsocks, to change the port you have to change it in docker [`compose.yml`](https://github.com/AlirezaDastyar/shadowsocks-ansible/blob/main/compose.yml#L6)
## Run it
Run the following command and provide the root password for ssh

`ansible-playbook setup.yml -i inventory.ini -k`
