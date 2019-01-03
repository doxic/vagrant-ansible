# -*- mode: ruby -*-
# # vi: set ft=ruby :

# based on https://blog.scottlowe.org/2014/10/22/multi-machine-vagrant-with-yaml/

# This guide is optimized for Vagrant 1.7 and above.
# Although versions 1.6.x should behave very similarly, it is recommended
# to upgrade instead of disabling the requirement below.
Vagrant.require_version ">= 1.7.0"
VAGRANTFILE_API_VERSION = "2"

# Require YAML module
require 'yaml'

# Read YAML file with box details
servers = YAML.load_file('servers.yml')

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Iterate through entries in YAML file
  servers.each_with_index do |servers, index|
    config.vm.define servers["name"] do |srv|
      srv.vm.box = servers["box"]

      # Disable the new default behavior introduced in Vagrant 1.7, to
      # ensure that all Vagrant machines will use the same SSH key pair.
      # See https://github.com/hashicorp/vagrant/issues/5005
      config.ssh.insert_key = false

      srv.vm.network "private_network", ip: servers["ip"]

      srv.vm.provider :virtualbox do |vb|
        vb.name = servers["name"]
        vb.memory = servers["ram"]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
      end # end srv.vm.provider

      # Enable provisioning with Ansible.
      # https://github.com/hashicorp/vagrant/issues/1784
      if index == servers.size - 1
        config.vm.provision "ansible" do |ansible|
          ansible.compatibility_mode = "2.0"
          ansible.playbook = "playbook.yml"
          ansible.galaxy_role_file = "requirements.yml"
          ansible.limit = "all"
          ansible.become = true
        end # end config.vm.provision
      end # end if index

    end  # end config.vm.define
  end # end servers.each_with_index
end # Vagrant.configure
