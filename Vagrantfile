Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_version = "20230607.0.0"

  config.vm.network "private_network", ip: "192.168.56.10"

  ENV['VAGRANT_LOG'] = 'info'

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y docker.io docker-compose
    systemctl enable docker
    systemctl start docker

    if ! getent group docker | grep -q vagrant; then
      usermod -aG docker vagrant
    fi
    
    chmod 666 /var/run/docker.sock
  SHELL

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "main.yml"
    #ansible.verbose = "vv"
  end
end