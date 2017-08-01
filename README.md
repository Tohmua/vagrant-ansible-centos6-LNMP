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
After changing any ansible settings just run `vagrant provision` to propagate the changes to the VM.

### Requirements
- **git**

  Getting started: [wiki](https://en.wikipedia.org/wiki/Git)

- **Vagrant**

  Install vagrant instructions can be found here: [vagrant](https://www.vagrantup.com/downloads.html)

- **VirtualBox**

  Install VirtualBox, instructions can be found here: [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

- **Ansible**

  Install Ansible, instructions can be found here: [Ansible](http://docs.ansible.com/ansible/intro_installation.html#installing-the-control-machine)

### Config File Location Inside The Virtual Machine
**PHP set up** uses remi-safe repository with PHP-FPM FastCGI process
* php.ini file is at : `/opt/remi/php56/root/etc/php.ini`
* error log setting : `/var/log/php-fpm/error.log`
* to restart PHP-FPM : `sudo service php-56-php-fpm restart`
* Xdebug executable : `/opt/remi/php56/root/usr/lib64/php/modules/xdebug.so`
* xdebug.ini file at : `/opt/remi/php56/root/etc/php.d/15-xdebug.ini`
**Nginx**
* nginx configuration : `/etc/nginx/nginx.conf`
* to restart nginx : `sudo service nginx restart`
