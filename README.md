# Centos 6 LNMP Stack
- Centos 6.5
- NginX
- MySQL 5.7
- PHP 5.6/7.2/7.3
- Node
- NPM
- Memcache

### Run
```
cp ansible/group_vars/all.example ansible/group_vars/all
vagrant plugin install vagrant-vbguest
vagrant up
```

### Add Virtual Hosts
Add a new entry to the `virtual_hosts` dictionary in the `ansible/group_vars/all` file. Set the `host_name` to the virtual host that you would like to use.

Add the following line `192.168.33.35 {host_name}` (where the `{host_name}` is the one from the `all` file) to your hosts file `/etc/hosts`

### Change PHP Versions
Edit `ansible/group_vars/all` with your favourite editor and change
the `php_version` variable. 5.6 and 7.2 are the only allowed version numbers at this time.

### Update Dependencies
After changing any ansible settings just run `vagrant up --provision` to propagate the changes to the VM.

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
**Nginx**
- error log setting : `/var/log/php-fpm/error.log`
- nginx configuration : `/etc/nginx/nginx.conf`

**PHP**
- php.ini file is at : `/opt/remi/php56/root/etc/php.ini`
- Xdebug executable : `/opt/remi/php56/root/usr/lib64/php/modules/xdebug.so`
- xdebug.ini file at : `/opt/remi/php56/root/etc/php.d/15-xdebug.ini`

**CentOS**
- restart nginx : `sudo service nginx restart`
- to restart PHP-FPM : `sudo service php56-php-fpm restart`

### Running multiple machines
- Duplicate the `"default"` block in `Vagrantfile`
- Rename `"default"` to something else (e.g. `"newVm"`)
- Change both the host port (from `6612`) and the ip (from `192.168.33.35`)
- Access new vm using `vagrant up newVm` and `vagrant ssh newVm`
