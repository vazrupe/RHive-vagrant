# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  
  config.vm.define "hadoop" do |hadoop|
    hadoop.vm.provider "virtualbox" do |vb|
      vb.name = "hadoop"
      vb.memory = "1024"
    end
    # hadoop.vm.network "forwarded_port", guest: 80, host: 8080
    hadoop.vm.network "private_network", ip: "192.168.33.10"
    # hadoop.vm.network "public_network"
    hadoop.vm.hostname = "hadoop"
    
    hadoop.vm.synced_folder "script", "/scripts"
  end
end