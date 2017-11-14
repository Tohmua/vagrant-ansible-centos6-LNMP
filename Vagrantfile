# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.define "default" do |default|
    default.vm.box = "flat/centos6.5"

    default.vm.network "forwarded_port", guest: 3306, host: 6612

    default.vm.network :private_network, ip: "192.168.33.35"

    default.vm.synced_folder "www/", "/vagrant", type: "nfs"

    default.vm.provider "virtualbox" do |v|
      v.memory = 2048
      v.customize [ "guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000 ]
    end

    default.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/install.yml"
      # ansible.inventory_path = "ansible/hosts"
      ansible.verbose = true
      ansible.sudo = true
    end
  end
end
