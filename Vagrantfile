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
      cat << EOF > /etc/hosts
192.168.33.20   apache
192.168.33.21   mysql
192.168.33.22   jenkins
EOF
      cat << EOF > /etc/ansible/hosts
[web]
apache
[db]
mysql
[ci]
jenkins
EOF
    SHELL
  end
  config.vm.define "slave1" do |w|
    w.vm.box = "bento/ubuntu-18.04"
    w.vm.hostname = "apache"
    w.vm.network "private_network", ip: "192.168.33.20"
    w.vm.network "forwarded_port", guest: 80, host: 8000
    w.vm.provision "shell", inline: <<-SHELL
    python --version
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
    sudo update-alternatives --set python /usr/bin/python3.6
    cat << EOF > /etc/hosts
192.168.33.10   ansible
EOF
    SHELL
  end
  config.vm.define "slave2" do |d|
    d.vm.box = "bento/ubuntu-18.04"
    d.vm.hostname = "mysql"
    d.vm.network "private_network", ip: "192.168.33.21"
    d.vm.provision "shell", inline: <<-SHELL
      python --version
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << EOF > /etc/hosts
192.168.33.10   ansible
EOF
    SHELL
  end
  config.vm.define "slave3" do |j|
    j.vm.box = "bento/ubuntu-18.04"
    j.vm.hostname = "jenkins"
    j.vm.network "private_network", ip: "192.168.33.22"
    j.vm.network "forwarded_port", guest: 80, host: 8080
    j.vm.provision "shell", inline: <<-SHELL
      python --version
      sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
      sudo update-alternatives --set python /usr/bin/python3.6
      cat << EOF > /etc/hosts
192.168.33.10   ansible
EOF
    SHELL
  end
end
