# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  # config.vm.box = "ubuntu/vivid64"
  # config.vm.box = "relativkreativ/centos-7-minimal"
  # config.vm.box = "box-cutter/fedora22"
  # config.vm.box = "puppetlabs/centos-6.6-64-nocm"

  BOX_COUNT = 1
  (1..BOX_COUNT).each do |machine_id|
    config.vm.define "kapacitor#{machine_id}" do |machine|
      machine.vm.hostname = "kapacitor#{machine_id}"
      machine.vm.network "private_network", ip: "10.0.3.#{1+machine_id}", virtualbox__intnet: true
      
      machine.vm.provider "virtualbox" do |v|
        v.memory = 512
        v.cpus = 1
      end

      if machine_id == BOX_COUNT
        machine.vm.provision "ansible" do |ansible|
          ansible.limit = 'all'
          ansible.playbook = "test.yml"
          ansible.sudo = true
          ansible.host_key_checking = false
          ansible.extra_vars = {
            is_vagrant: true,
          }
        end
      end
      
    end
  end
end
