Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "cp-cp1" do |node|
    node.vm.hostname = "cp-cp1"
    node.vm.network "private_network", ip: "192.168.33.10"
    node.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end
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
          ansible.limit = "all"
          ansible.playbook = "playbook.yml"
        end
      end

    end
  end
end
