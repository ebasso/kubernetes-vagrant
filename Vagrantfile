# -*- mode: ruby -*-
# vi: set ft=ruby :
IMAGE_NAME = "centos/7"
IMAGE_VERSION = "1804.02"

NODES_NUM = 2

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap/common.sh"

  # Kubernetes Master Server
  config.vm.define "master" do |master|
    master.vm.box = IMAGE_NAME
    master.vm.box_version = IMAGE_VERSION
    master.vm.hostname = "master.k8s.com"
    master.vm.network "private_network", ip: "172.42.42.100"
    master.vm.provider "virtualbox" do |v|
      v.name = "master"
      v.memory = 2048
      v.cpus = 2
      v.customize ["modifyvm", :id, "--vram", "6"]
      v.customize ["modifyvm", :id, "--graphicscontroller", "vmsvga"]
      v.customize ["modifyvm", :id, "--audio", "none"]
      v.customize ["modifyvm", :id, "--groups", "/K8s"]
      #[--graphicscontroller none|vboxvga|vmsvga|vboxsvga]
    end
    master.vm.provision "shell", path: "bootstrap/master.sh"
  end

  # Kubernetes Worker Nodes
  (1..NODES_NUM).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = IMAGE_NAME
      node.vm.box_version = IMAGE_VERSION
      node.vm.hostname = "node#{i}.k8s.com"
      node.vm.network "private_network", ip: "172.42.42.10#{i}"
      node.vm.provider "virtualbox" do |v|
        v.name = "node#{i}"
        v.memory = 1024
        v.cpus = 1
        v.customize ["modifyvm", :id, "--vram", "6"]
        v.customize ["modifyvm", :id, "--graphicscontroller", "vmsvga"]
        v.customize ["modifyvm", :id, "--audio", "none"]
        v.customize ["modifyvm", :id, "--groups", "/K8s"]
      end
      node.vm.provision "shell", path: "bootstrap/node.sh"
    end
  end

end
