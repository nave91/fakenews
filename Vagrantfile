# -*- mode: ruby -*-

VAGRANTFILE_API_VERSION = "2"

require 'rbconfig'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.forward_agent = true
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_check_update = true
  config.vm.network "private_network", ip: "10.1.1.100"
  config.vm.network :forwarded_port, host: 7654, guest: 7654

  config.vm.synced_folder ".", "/home/vagrant/fakenews", id: "vagrant-root", type: "nfs", mount_options: ['nfsvers=3', 'actimeo=1']
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provision/local.yml"
        ansible.ask_vault_pass = false
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--nictype1", "Am79C973"]
    v.customize ["modifyvm", :id, "--nictype2", "Am79C973"]
    v.memory = 2048
    v.cpus = 4
  end
end
