# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-7.5"
  config.vm.define "master" do |m|
    m.vm.hostname = "ansible"
    m.vm.network "private_network", ip: "192.168.33.20"
    m.vm.provision "shell", inline: <<-SHELL
      echo "Installing Ansible"
      yum install epel-release -y
      yum install ansible vim -y
      cat << STOP > /etc/hosts
127.0.0.1    ansible
192.168.33.21    web
192.168.33.22    mysql
192.168.33.23    nginx
192.168.33.24    jenkins
STOP
      cat << STOP > /etc/ansible/hosts
[webserver]
web
[dbserver]
mysql
[balancer]
nginx
[ci]
jenkins
STOP
    SHELL
  end
  config.vm.define "slave1" do |s|
    s.vm..box = "bento/ubuntu-18.04"
    s.vm.hostname = "web"
    s.vm.network "private_network", ip: "192.168.33.21"
    s.vm.network "forwarded_port", guest: 80, host: 8080
    s.vm.provision "shell", inline: <<-SHELL
      cat << STOP > /etc/hosts
127.0.0.1    web
192.168.33.20    ansible
STOP
    SHELL
    s.vm.provision "ansible" do |ansible|
      ansible.playbook = "web.yml"
    end
  end
  config.vm.define "slave2" do |s|
    s.vm..box = "bento/ubuntu-18.04"
    s.vm.hostname = "mysql"
    s.vm.network "private_network", ip: "192.168.33.22"
    s.vm.provision "shell", inline: <<-SHELL
      cat << STOP > /etc/hosts
127.0.0.1    mysql
192.168.33.20    ansible
STOP
    SHELL
    s.vm.provision "ansible" do |ansible|
      ansible.playbook = "db.yml"
    end
  end
  config.vm.define "slave3" do |s|
    s.vm..box = "bento/ubuntu-18.04"
    s.vm.hostname = "nginx"
    s.vm.network "private_network", ip: "192.168.33.23"
    s.vm.network "forwarded_port", guest: 80, host: 8000
    s.vm.provision "shell", inline: <<-SHELL
      cat << STOP > /etc/hosts
127.0.0.1    nginx
192.168.33.20    ansible
STOP
    SHELL
    s.vm.provision "ansible" do |ansible|
      ansible.playbook = "nginx.yml"
    end
  end
  config.vm.define "slave4" do |s|
    s.vm..box = "bento/ubuntu-18.04"
    s.vm.hostname = "jenkins"
    s.vm.network "private_network", ip: "192.168.33.24"
    s.vm.network "forwarded_port", guest: 80, host: 8001
    s.vm.provision "shell", inline: <<-SHELL
      cat << STOP > /etc/hosts
127.0.0.1    jenkins
192.168.33.20    ansible
STOP
    SHELL
    s.vm.provision "ansible" do |ansible|
      ansible.playbook = "jenkins.yml"
    end
  end
end
