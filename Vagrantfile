# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.hostname = "local.cloudvm.com"
  config.vm.network :private_network, ip: "192.168.4.40"

  config.vm.box = "ubuntu1204"
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/ubuntu-server-12042-x64-vbox4210-nocm.box"

  config.vm.synced_folder "/Users/jgeerling/Sites/drupal", "/drupal",
    type: "rsync",
    rsync__auto: "true",
    rsync__exclude: ".git/",
    rsync__args: ["--verbose", "--archive", "--delete", "-z", "--chmod=ugo=rwX"],
    id: "drupal"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.sudo = true
  end

  # VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--name", "local.cloudvm.com"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", 1024]
    v.customize ["modifyvm", :id, "--cpus", 2]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :cloudvm do |cloudvm_config|
  end

end
