# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "master" do |m|
    m.vm.box = "bento/centos-7.5"
    m.vm.hostname = "ansible"
    m.vm.network "private_network", ip: "192.168.33.10"
    m.vm.provision "shell", inline: <<-SHELL
      sudo yum install epel-release -y
      sudo yum install ansible -y
      cat << STOP > /etc/hosts
192.168.33.20   apache
192.168.33.21   mysql
192.168.33.22   jenkins
STOP
      cat << STOP > /etc/ansible/hosts
[web]
apache
[db]
mysql
[ci]
jenkins
STOP
    SHELL
  end
  config.vm.define "slave1" do |s|
    s.vm.box = "bento/ubuntu-18.04"
    s.vm.hostname = "apache"
    s.vm.network "private_network", ip: "192.168.33.20"
    s.vm.network "forwarded_port", guest: 80, host: 8000
    s.vm.provision "shell", inline: <<-SHELL
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << STOP > /etc/hosts
192.168.33.10   ansible
STOP
    SHELL
  end
  config.vm.define "slave2" do |s|
    s.vm.box = "bento/ubuntu-18.04"
    s.vm.hostname = "mysql"
    s.vm.network "private_network", ip: "192.168.33.21"
    s.vm.provision "shell", inline: <<-SHELL
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << STOP > /etc/hosts
192.168.33.10   ansible
STOP
    SHELL
  end
  config.vm.define "slave3" do |s|
    s.vm.box = "bento/ubuntu-18.04"
    s.vm.hostname = "jenkins"
    s.vm.network "private_network", ip: "192.168.33.22"
    s.vm.network "forwarded_port", guest: 80, host: 8080
    s.vm.provision "shell", inline: <<-SHELL
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << STOP > /etc/hosts
192.168.33.10   ansible
STOP
    SHELL
  end
end
