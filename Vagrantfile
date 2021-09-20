# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "cp-cp1" do |node|
    node.vm.hostname = "cp-cp1"
    node.vm.network "private_network", ip: "192.168.33.10"
    node.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
    #config.vm.provision "ansible" do |ansible|
    #  ansible.playbook = "playbook.yml"
    #end
  end

  (1..3).each do |i|
    config.vm.define "c1-node#{i}" do |node|
      node.vm.hostname = "c1-node#{i}"
      node.vm.network "private_network", ip: "192.168.33.1#{i}"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 2
      end
      if i == 3
        node.vm.provision :ansible do |ansible|
        # Disable default limit to connect to all the machines
        ansible.limit = "all"
        ansible.playbook = "playbook.yml"
      end
    end
    end
  end
    
end
