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
Add a new entry to the `virtual_hosts` dictionary in the `ansible/group_vars/all` file. Set the `host_name` to the 
virtual host that you would like to use.

Add the following line `192.168.33.35 {host_name}` (where the `{host_name}` is the one from the `all` file) to your 
hosts file `/etc/hosts` on your host machine.

### Change PHP Versions
Edit `ansible/group_vars/all` with your favourite editor and change
the `php_version` variable. 5.6, 7.2 and 7.3 are the only allowed version numbers at this time.

### Provision with Xdebug enabled
Edit `ansible/group_vars/all` with your favourite editor and change
the `xdebug` variable from false (default) to true.

### Update Dependencies / Reprovision
**After changing any ansible settings you must run `vagrant up --provision` to propagate the changes to the VM**.

### Requirements
- **git**

  Getting started: [wiki](https://en.wikipedia.org/wiki/Git)

- **Vagrant**

  Install vagrant instructions can be found here: [vagrant](https://www.vagrantup.com/downloads.html)

- **VirtualBox**

  Install VirtualBox, instructions can be found here: [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

- **Ansible**

  Install Ansible, instructions can be found here: [Ansible](http://docs.ansible.com/ansible/intro_installation.html#installing-the-control-machine)

### Virtual machine config files and CLI commands
**Nginx**
- php error log setting : `/var/log/php-fpm/error.log`
- nginx configuration : `/etc/nginx/nginx.conf`
- restart nginx : `sudo service nginx restart`

**PHP 5.6**
- php.ini file is at : `/opt/remi/php56/root/etc/php.ini`
- additional ini files scan directory at : `/opt/remi/php56/root/etc/php.d/`
- to restart php : `sudo service php56-php-fpm restart`

**PHP 7.2**
- php.ini file is at : `/etc/opt/remi/php72/php.ini`
- additional ini files scan directory at : `/etc/opt/remi/php72/php.d/`
- to restart php : `sudo service php72-php-fpm restart`

**PHP 7.3**
- php.ini file is at : `/etc/opt/remi/php73/php.ini`
- additional ini files scan directory at : `/etc/opt/remi/php73/php.d/`
- to restart php : `sudo service php73-php-fpm restart`

### Running multiple applications and virtual machines
- To run two separate virtual machines from two separate copies of the vagrant-ansible-centos6-LNMP codebase you will 
need to adjust the port and ip settings in the second `Vagrantfile` to avoid clashes with your first virtual machine. 
For example change port 6612 and ip 192.168.33.35 to:
 ```
default.vm.network "forwarded_port", guest: 3306, host: 6613
default.vm.network :private_network, ip: "192.168.33.36"
```
You will also need to amend the entry in `ansible/hosts` file to match the changed ip address. When creating virtual 
hosts in accordance with the "Add Virtual Hosts" instructions above use the changed ip address in /etc/hosts entries.
- To run multiple virtual machines from a single copy of the vagrant-ansible-centos6-LNMP codebase from a single 
Vagrant file you will need to:
    - Duplicate the `"default"` block in `Vagrantfile`
    - Rename `"default"` to something else (e.g. `"newVm"`)
    - Change both the host port (from `6612`) and the ip (from `192.168.33.35`) to avoid clashes (see above)
    - Change entry in `ansible/hosts` to match new name and ip
    - Access new vm using `vagrant up newVm` and `vagrant ssh newVm`
