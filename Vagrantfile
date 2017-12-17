# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider :virtualbox do |v|
      v.customize [
          "modifyvm", :id,
          "--name", "default",
          "--memory", 512,
          "--natdnshostresolver1", "on",
          "--cpus", 1,
      ]
  end

  config.vm.hostname = "vagrant-centos7"
  config.vm.box = "centos/7"
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.network "private_network", ip: "11.0.0.2"
  config.ssh.forward_agent = true

  config.vm.synced_folder "/var/www", "/var/www"

  ## Basic functionality
  config.vm.provision "shell", inline: <<-SHELL
     yum update -y
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    ansible.limit = 'all'
  end
end
