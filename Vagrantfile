# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.define "vm1" do |vm1|
    vm1.vm.box = "bento/ubuntu-22.04"
    vm1.vm.hostname = "redis-1"
   end
  config.vm.define "vm2" do |vm2|
    vm2.vm.box = "bento/ubuntu-22.04"
    vm2.vm.hostname = "redis-2"
   end 
  config.vm.define "vm3" do |vm3|
    vm3.vm.box = "bento/ubuntu-22.04"
    vm3.vm.hostname = "redis-3"
   end
  config.vm.network "public_network"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    #vb.cpus   = 2
  end
  config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt install -y ntp ntpdate lsb-release curl gpg
    ntpdate -u 0.ubuntu.pool.ntp.org
    timedatectl set-timezone Europe/Chisinau
  SHELL
end
