# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'

VAGRANTFILE_API_VERSION = "2"
Vagrant.require_version ">= 1.5.0"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "centos/7"

  # Turn off shared folders
  config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true

  # Begin testvm
  config.vm.define "vmtest" do |config|
    config.vm.hostname = "owncloud-aio"
    # config.vm.provision "shell", inline: <<-SHELL
    #   sudo yum install -y net-tools
    #   SHELL
    config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbooks/owncloud_node.yml"
    ansible.inventory_path = "inventory/"
    ansible.limit = "owncloud-vagrant"
    end 
    # eth1
    config.vm.network "private_network", ip: "10.0.0.10"

    config.vm.provider "libvirt" do |libvirt|
      #use the storage pool named external
      #libvirt.storage_pool_name = "external"
      libvirt.driver = "kvm"
      libvirt.memory = 1024
      libvirt.cpus = 2
    end
  end

end

