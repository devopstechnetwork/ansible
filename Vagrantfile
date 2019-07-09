# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "master" do |m|
    m.vm.box = "bento/centos-7.5"
    m.vm.hostname = "ansible"
    m.vm.network "private_network", ip: "192.168.33.10"
    m.vm.provision "shell", inline: <<-SHELL
      sudo yum update -y
      sudo yum install epel-release -y
      sudo yum install ansible -y
    SHELL
  end
  config.vm.define "slaveOne" do |w|
    w.vm.box = "bento/ubuntu-18.04"
    w.vm.hostname = "apache"
    w.vm.network "private_network", ip: "192.168.33.20"
    w.vm.network "forwarded_port", guest: 80, host: 8000
  end
  config.vm.define "slaveTwo" do |d|
    d.vm.box = "bento/ubuntu-18.04"
    d.vm.hostname = "mysql"
    d.vm.network "private_network", ip: "192.168.33.21"
  end
  config.vm.define "slaveThree" do |j|
    j.vm.box = "bento/ubuntu-16.04"
    j.vm.hostname = "jenkins"
    j.vm.network "private_network", ip: "192.168.33.22"
    j.vm.network "forwarded_port", guest: 80, host: 8080
  end
end
