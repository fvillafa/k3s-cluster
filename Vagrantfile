# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.define "master" do |master|
    master.vm.box = "alpine-k3s"
    master.vm.network "private_network", ip: "192.168.56.2"

    master.vm.provision "shell", inline: <<-SHELL

    curl -sfL https://get.k3s.io | K3S_NODE_NAME="master" INSTALL_K3S_EXEC="--bind-address=192.168.56.2 --node-external-ip=192.168.56.2 \
    --flannel-iface=eth1" K3S_TOKEN="UDm7hBK1AEKgVOuQEyLb" K3S_KUBECONFIG_MODE="644" sh -s -

    SHELL
  end

  config.vm.define "node" do |node|
    node.vm.box = "alpine-k3s"
    node.vm.network "private_network", ip: "192.168.56.3"

    node.vm.provision "shell", inline: <<-SHELL

    curl -sfL https://get.k3s.io | K3S_NODE_NAME="node" INSTALL_K3S_EXEC="--node-external-ip=192.168.56.3 \
    --flannel-iface=eth1" K3S_TOKEN="UDm7hBK1AEKgVOuQEyLb" K3S_URL=https://192.168.56.2:6443 sh -s -

    SHELL
  end

end
