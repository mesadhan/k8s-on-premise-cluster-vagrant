# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # K8S Master Server
  config.vm.define "master" do |master_node|
    master_node.vm.box = "centos/7"
    master_node.vm.hostname = "master.example.com"
    master_node.vm.network "private_network", ip: "172.42.42.100"
    master_node.vm.provider "virtualbox" do |v|
      v.name = "master"
      v.memory = 2048
      v.cpus = 2
    end
    master_node.vm.provision "shell", path: "master.sh"
  end


  NodeCount = 2
  # K8S Worker Nodes
  (1..NodeCount).each do |i|
    config.vm.define "worker#{i}" do |worker_node|
      worker_node.vm.box = "centos/7"
      worker_node.vm.hostname = "worker#{i}.example.com"
      worker_node.vm.network "private_network", ip: "172.42.42.10#{i}"
      worker_node.vm.provider "virtualbox" do |v|
        v.name = "worker#{i}"
        v.memory = 1024
        v.cpus = 1
      end
      worker_node.vm.provision "shell", path: "worker.sh"
    end
  end

end
