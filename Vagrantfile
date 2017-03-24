# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "flat/centos6.5"

  config.vm.network "forwarded_port", guest: 3306, host: 6612

  config.vm.network :private_network, ip: "192.168.33.35"

  config.vm.synced_folder ".", "/vagrant", type: "nfs"

  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.customize [ "guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000 ]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/install.yml"
    ansible.inventory_path = "ansible/hosts"
    ansible.verbose = true
    ansible.sudo = true
  end
end
