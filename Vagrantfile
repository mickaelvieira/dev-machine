# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "cloudtoad/xenial_server_base"

    # config.vm.hostname = ""

    config.vm.network :private_network, ip: "10.0.15.74"

    config.vm.synced_folder "~/dev", "/srv/", :owner=> 'www-data', :group=>'www-data', :mount_options => ['dmode=775', 'fmode=664']
    # config.vm.synced_folder "~/dev", "/srv/", type: "nfs"

    config.vm.provider "virtualbox" do |vb|
        vb.name = 'DevMachine'
        vb.customize ["modifyvm", :id, "--memory", "2048"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--audio", "none", "--usb", "off", "--usbehci", "off"]
        vb.customize ["guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000]
    end

    config.vm.provision "file", source: "ansible/ansible.cfg", destination: "~/.ansible.cfg"

    config.vm.provision "ansible" do |ansible|
        ansible.limit = "development"
        ansible.verbose = true
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/hosts"
    end
end
