# Centos 6 LNMP Stack
- Centos 6.5
- NginX
- MySQL 5.7
- PHP 5.6
- Node
- NPM

### Run
```
cp ansible/group_vars/all.example ansible/group_vars/all
vagrant plugin install vagrant-vbguest
vagrant up
```

### Update Dependencies
After changing any ansible settings just run `vagrant provision` to propergate the changes to the VM.

### Requirements
- **git**

  Getting started: [wiki](https://en.wikipedia.org/wiki/Git)

- **Vagrant**

  Install vagrant instructions can be found here: [vagrant](https://www.vagrantup.com/downloads.html)

- **VirtualBox**

  Install VirtualBox, instructions can be found here: [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

- **Ansible**

  Install Ansible, instructions can be found here: [Ansible](http://docs.ansible.com/ansible/intro_installation.html#installing-the-control-machine)
