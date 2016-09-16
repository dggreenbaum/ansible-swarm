# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/wily64"

  # Machine-specific provider-specific config (names)
  config.vm.define "kv" do |machineconfig|
    machineconfig.vm.provider "virtualbox" do |vb|
      vb.name = "kv"
    end
    machineconfig.vm.network "private_network", ip: "192.168.33.10"
  end

  config.vm.define "c0-master" do |machineconfig|
    machineconfig.vm.provider "virtualbox" do |vb|
      vb.name = "c0-master"
    end
    machineconfig.vm.network "private_network", ip: "192.168.33.11"
  end

  config.vm.define "c0-n1" do |machineconfig|
    machineconfig.vm.provider "virtualbox" do |vb|
      vb.name = "c0-n1"
    end
    machineconfig.vm.network "private_network", ip: "192.168.33.12"
  end

  config.vm.define "c0-n2" do |machineconfig|
    machineconfig.vm.provider "virtualbox" do |vb|
      vb.name = "c0-n2"
    end
    machineconfig.vm.network "private_network", ip: "192.168.33.13"
    machineconfig.vm.provision :ansible do |ansible|
      ansible.playbook  = "playbook.yml"
      ansible.verbose   = "vv"
      ansible.limit     = "all" # or only "nodes" group, etc.
      ansible.groups    = {
        "kv" => ["kv"],
        "swarm_master" => ["c0-master"],
        "swarm_member" => ["c0-master", "c0-n1", "c0-n2"]
      }
   end
  end

  # Common provider-specific config
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "512"
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--vram", "8"]
  end

end
