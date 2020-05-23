# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

config = YAML.load_file('config.yaml')

requirements = YAML.load_file('provisioning/requirements.yml')

#ansibleProvisioner = Vagrant::Util::Platform.windows? ? :"ansible_local" : :"ansible"
ansibleProvisioner = "ansible_local"

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"

  # create forwarded ports for http, https and mssql services
  #config.vm.network "forwarded_port", guest: 80, host: 8080, protocol: "tcp"    #http

  config.vm.define "box" do |box|
    box.vm.network :private_network, ip: "192.168.33.13"
    box.vm.hostname = "box"

    # enable synced folder
    box.vm.synced_folder  ".", "/vagrant"

    # # install git to fetch requirements when using ansible_local provisioning
    if "ansible_local".eql? ansibleProvisioner
      # provisioning with shell command: install git package
      #  git is needed for ansible roles fetched directly from git repository
      box.vm.provision :shell, inline: <<-SHELL
        PACKAGE=git
        if ! dpkg --get-selections | grep -q $PACKAGE; then
          echo "Installing git ..."
          sudo apt install git
        fi
      SHELL
    end

    # configure provisioning
    box.vm.provision ansibleProvisioner do |ansible|
       ansible.playbook = "provisioning/playbook.yml"                    # provisioning definition

      if "ansible_local".eql? ansibleProvisioner
        # check for elements in requirements file
        #  ansible-galaxy fails when the file has no elements
        unless requirements.nil?
          ansible.galaxy_role_file = "provisioning/requirements.yml"    # requirements definition for provisioning
        end
      end

    end

  end

end
