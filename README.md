# Acquia Cloud VM

I use this VM to test things in an environment close to that of Acquia's Cloud servers, following the guide at [Acquia Cloud technology platform and supported software](https://docs.acquia.com/cloud/arch/tech-platform).

The following is included inside this VM:

  - Ubuntu 12.04 (Precise)
  - Apache 2.2.22
  - MySQL 5.5.x
  - PHP 5.3.x (5.5.x configurable)
  - Varnish 3.x
  - Memcached 1.4.x
  - XDebug
  - Composer
  - Drush 6.x
  - Git 1.9.x
  - (More to come...).

## Usage

  1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads), [Vagrant](https://www.vagrantup.com/downloads.html), and [Ansible](http://docs.ansible.com/intro_installation.html):
    - `$ brew cask install virtualbox vagrant`
    - `$ brew install ansible`
  2. Install all the roles listed in `playbook.yml` with the command `$ ansible-galaxy install [role name]`
  2. Copy `example.config.yml` to `config.yml` (your local `config.yml` will be ignored by Git and you can modify it to suit your needs).
  3. (From the same directory as this README file) run `$ vagrant up`

*This assumes you have [Homebrew](http://brew.sh/) installed and have `cask` installed (`brew tap caskroom/cask && brew install brew-cask` to install). On a Linux or Windows computer, you will need to install VirtualBox, Vagrant and Ansible according to the linked guides in step 1. This VM is not currently supported on Windows, but if you'd like support, please file an issue.*

**Note**: Do NOT use the included Ansible playbook for production infrastructure unless you understand the security implications and have configured secure passwords, a firewall, etc. This VM and playbook are meant to help you replicate the Aquia Cloud environment locally, not to replicate the Acquia Cloud on other public infrastructure. You have been warned!

## Customization

Please see the available VM customization options inside `config.yml`. You can easily define folder mappings inside this folder, as well as change settings like RAM/CPU allocation, the hostname and IP address of the VM, and even things like Apache and Varnish ports.

Things like hosts file configuration (changing your local system's hosts file to point to this VM's IP address for development hostnames) are left to you to manage. My goal is to make this VM configuration extremely flexible and lightweight.

## Syncing Files

This VM uses Vagrant's built-in rsync-based folder syncing (which is currently one-way), and pushes your files into the VM every time you do a `vagrant up` or `vagrant reload`. To initiate a one-time sync, use `vagrant rsync`, or to continuously monitor your local files for changes (and automatically sync them to the VM), use `vagrant rsync-auto`.

## TODO

  - Add Solr (`geerlingguy.tomcat6` + `geerlingguy.solr`)
  - Add XHProf (`geerlingguy.xhprof`)
  - Add PHPMyAdmin (`geerlingguy.phpmyadmin`)
  - Add other utilities and helpful tooling

## Author Information

This VM was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
