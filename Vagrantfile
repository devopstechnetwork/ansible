# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "master" do |m|
    m.vm.box = "bento/centos-7.5"
    m.vm.hostname = "ansible"
    m.vm.network "private_network", ip: "192.168.33.20"
    m.vm.provision "shell", inline: <<-SHELL
      sudo yum install epel-release -y
      sudo yum install ansible -y
      cat << STOP > /etc/hosts
127.0.0.1    ansible
192.168.33.20   web1
192.168.33.21   web2
192.168.33.22   mysql
192.168.33.23   nginx
STOP
      cat << STOP > /etc/ansible/hosts
[webserver]
web
[dbserver]
mysql
[loadbalancer]
nginx
[other]
jenkins
STOP
    SHELL
  end
  config.vm.define "slave1" do |s|
    s.vm.box = "bento/ubuntu-18.04"
    s.vm.hostname = "web"
    s.vm.network "private_network", ip: "192.168.33.21"
    s.vm.network "forwarded_port", guest: 80, host: 8000
    s.vm.provision "shell", inline: <<-SHELL
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << STOP > /etc/hosts
127.0.0.1    web
192.168.33.10   ansible
STOP
    SHELL
  end
  config.vm.define "slave2" do |s|
    s.vm.box = "bento/ubuntu-18.04"
    s.vm.hostname = "mysql"
    s.vm.network "private_network", ip: "192.168.33.22"
    s.vm.provision "shell", inline: <<-SHELL
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << STOP > /etc/hosts
127.0.0.1    mysql
192.168.33.10   ansible
STOP
    SHELL
  end
  config.vm.define "slave3" do |s|
    s.vm.box = "bento/ubuntu-18.04"
    s.vm.hostname = "nginx"
    s.vm.network "private_network", ip: "192.168.33.23"
    s.vm.provision "shell", inline: <<-SHELL
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << STOP > /etc/hosts
127.0.0.1    nginx
192.168.33.10   ansible
STOP
    SHELL
  end
  config.vm.define "slave4" do |s|
    s.vm.box = "bento/ubuntu-18.04"
    s.vm.hostname = "jenkins"
    s.vm.network "private_network", ip: "192.168.33.24"
    s.vm.network "forwarded_port", guest: 80, host: 8001
    s.vm.provision "shell", inline: <<-SHELL
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << STOP > /etc/hosts
127.0.0.1    jenkins
192.168.33.10   ansible
STOP
    SHELL
  end
end
