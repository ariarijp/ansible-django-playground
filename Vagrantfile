# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end
  config.vm.provision "shell", inline: <<-SHELL
    sed -i s/archive.ubuntu.com/ftp.jaist.ac.jp/ /etc/apt/sources.list
    apt-get update
    apt-get install -y build-essential python-dev python-setuptools language-pack-ja nginx
    easy_install pip
    pip install ansible
  SHELL

  config.vm.provision "shell", inline: "ansible-playbook -i 'localhost,' /vagrant/playbook.yml --connection=local", privileged: false
end
