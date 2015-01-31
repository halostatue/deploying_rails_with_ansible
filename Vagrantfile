# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure('2') do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.define :app_server do |node|
    node.vm.network 'forwarded_port', guest: 80, host: 10080

    node.vm.network 'private_network', ip: '10.0.0.100'

    node.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'provisioning/app_server.yml'
      ansible.inventory_path = 'vagrant_ansible_inventory'
      ansible.verbose  = 'v'
    end

    config.vm.provider "virtualbox" do |vb|
       vb.customize ["modifyvm", :id, "--memory", "1024"]
    end
  end

  config.vm.define :db_server do |node|
    node.vm.network 'private_network', ip: '10.0.0.101'
    node.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'provisioning/db_server.yml'
      ansible.inventory_path = 'vagrant_ansible_inventory'
      ansible.verbose  = 'v'
    end
  end
end
