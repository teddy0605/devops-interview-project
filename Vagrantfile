# -*- mode: ruby -*-
# vi: set ft=ruby :
 
Vagrant.configure("2") do |config|

  config.vm.box = "luisico/centos-7.5-docker"
  config.vm.box_version = "18.06.0"
  config.vm.hostname = "test"
  config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 8888, host: 8888

    config.vm.provider "virtualbox" do |v|
      v.check_guest_additions = false
      v.memory = 2048
      v.cpus = 2
      v.customize ["modifyvm", :id, "--vram", "16"]
    end

  config.vm.provision "shell", inline: <<-SHELL
    sudo yum update
    sudo yum install -y wget
    sudo yum install -y epel-release
    sudo yum install -y ansible
    sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
    sudo rpm --import http://pkg.jenkins.io/redhat/jenkins.io.key
    sudo yum install -y java-1.8.0-openjdk-devel
    sudo yum install -y jenkins
    sudo systemctl start jenkins
    sudo chkconfig jenkins on
    sudo systemctl stop firewalld
    sudo echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
  SHELL


  config.ssh.insert_key = false
end