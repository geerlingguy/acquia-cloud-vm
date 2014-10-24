# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
vconfig = YAML::load_file("./config.yml")

Vagrant.configure("2") do |config|
  config.vm.hostname = vconfig['vagrant_hostname']
  config.vm.network :private_network, ip: vconfig['vagrant_ip']

  config.vm.box = "ubuntu1204"
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/ubuntu-server-12042-x64-vbox4210-nocm.box"

  for synced_folder in vconfig['vagrant_synced_folders'];
    config.vm.synced_folder synced_folder['local_path'], synced_folder['destination'],
      type: "rsync",
      rsync__auto: "true",
      rsync__exclude: synced_folder['excluded_paths'],
      rsync__args: ["--verbose", "--archive", "--delete", "-z", "--chmod=ugo=rwX"],
      id: synced_folder['id']
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.sudo = true
  end

  # VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--name", vconfig['vagrant_hostname']]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", vconfig['vagrant_memory']]
    v.customize ["modifyvm", :id, "--cpus", vconfig['vagrant_cpus']]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :cloudvm do |cloudvm_config|
  end

end
