# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

MASTER_IP="192.168.56.2"
NODE_IP="192.168.56.3"

Vagrant.configure("2") do |config|

  config.vm.define "master" do |master|
    master.vm.box = "fvillafa/alpine-3.15-k3s"
    master.vm.network "private_network", ip: MASTER_IP

    master.vm.provision "shell", inline: <<-SHELL

    curl -sfL https://get.k3s.io | K3S_NODE_NAME="master" INSTALL_K3S_EXEC="--bind-address=#{MASTER_IP} --node-external-ip=#{MASTER_IP} \
    --flannel-iface=eth1" K3S_TOKEN="UDm7hBK1AEKgVOuQEyLb" K3S_KUBECONFIG_MODE="644" sh -s - && cp /etc/rancher/k3s/k3s.yaml /vagrant/kubeconfig.yaml

    SHELL
  end

  config.vm.define "node" do |node|
    node.vm.box = "fvillafa/alpine-3.15-k3s"
    node.vm.network "private_network", ip: NODE_IP

    node.vm.provision "shell", inline: <<-SHELL

    curl -sfL https://get.k3s.io | K3S_NODE_NAME="node" INSTALL_K3S_EXEC="--node-external-ip=#{NODE_IP} \
    --flannel-iface=eth1" K3S_TOKEN="UDm7hBK1AEKgVOuQEyLb" K3S_URL=https://#{MASTER_IP}:6443 sh -s -

    SHELL
  end

end
