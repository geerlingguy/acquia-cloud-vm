# Acquia Cloud VM

I use this VM to test things in an environment close to that of Acquia's Cloud servers, following the guide at [Acquia Cloud technology platform and supported software](https://docs.acquia.com/cloud/arch/tech-platform).

The following is included inside this VM:

  - Ubuntu 12.04 (Precise)
  - Apache 2.2.22
  - MySQL 5.5.x
  - PHP 5.3.x (5.4.x/5.5.x configurable)
  - PHPMyAdmin 3.4.x
  - Varnish 3.x
  - Memcached 1.4.x
  - XDebug
  - Composer
  - Drush 6.x
  - Git 1.9.x
  - Command-line tools like `curl`, `iftop`, `traceroute`, `htop`, `strace`, `vim` and more.

## Usage

  1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads), [Vagrant](https://www.vagrantup.com/downloads.html), and [Ansible](http://docs.ansible.com/intro_installation.html):
    - `$ brew cask install virtualbox vagrant`
    - `$ brew install ansible`
  2. Install all the roles required by this playbook with the command `$ ansible-galaxy install -r requirements.txt`
  2. Copy `example.config.yml` to `config.yml` (your local `config.yml` will be ignored by Git and you can modify it to suit your needs).
  3. (From the same directory as this README file) run `$ vagrant up`

*This assumes you have [Homebrew](http://brew.sh/) installed and have `cask` installed (`brew tap caskroom/cask && brew install brew-cask` to install). On a Linux or Windows computer, you will need to install VirtualBox, Vagrant and Ansible according to the linked guides in step 1. This VM is not currently supported on Windows, but if you'd like support, please file an issue.*

**Note**: Do NOT use the included Ansible playbook for production infrastructure unless you understand the security implications and have configured secure passwords, a firewall, etc. This VM and playbook are meant to help you replicate the Aquia Cloud environment locally, not to replicate the Acquia Cloud on other public infrastructure. You have been warned!

## Customization

Please see the available VM customization options inside `config.yml`. You can easily define folder mappings inside this folder, as well as change settings like RAM/CPU allocation, the hostname and IP address of the VM, and even things like Apache and Varnish ports.

Things like hosts file configuration (changing your local system's hosts file to point to this VM's IP address for development hostnames) are left to you to manage. My goal is to make this VM configuration extremely flexible and lightweight.

## Syncing Files

This VM uses Vagrant's built-in rsync-based folder syncing (which is currently one-way), and pushes your files into the VM every time you do a `vagrant up` or `vagrant reload`. To initiate a one-time sync, use `vagrant rsync`, or to continuously monitor your local files for changes (and automatically sync them to the VM), use `vagrant rsync-auto`.

## Connecting to MySQL

By default, this VM is set up so you can manage mysql databases on your own. The default root MySQL user credentials are `root` for username+password, but you could change the password via `config.yml`. I use the MySQL GUI [Sequel Pro](http://www.sequelpro.com/) (Mac-only) to connect and manage databases, then Drush to sync databases (sometimes I'll just do a dump and import, but Drush is usually quicker, and is easier to do over and over again when you need it).

### Connect using Sequel Pro (or a similar client):

  1. Use the SSH connection type.
  2. Set the following options:
    - MySQL Host: `127.0.0.1`
    - Username: `root`
    - Password: `root` (or whatever password you chose in `config.yml`)
    - SSH Host: `192.168.4.40` (or whatever IP you chose in `config.yml`)
    - SSH User: `vagrant`
    - SSH Key: (browse to your `~/.vagrant.d/` folder and choose `insecure_private_key`)

You should be able to connect as the root user and add, manage, and remove databases and users.

### Connect using PHPMyAdmin (built-in):

  1. Visit http://local.cloudvm.com/phpmyadmin (or substitute another vhost configured in `config.yml`).
  2. If prompted for a login, log in using the MySQL root credentials (`root`/`root` by default, or whatever password you chose in `config.yml`).

## Using XHProf to Profile Code

The easiest way to use XHProf to profile your PHP code on a Drupal site is to install the Devel module, then in Devel's configuration, check the 'Enable profiling of all page views and drush requests' checkbox. In the settings that appear below, set the following values:

  - **xhprof directory**: `/usr/share/php`
  - **XHProf URL**: `http://local.xhprof.com/` (assuming you have this set in `apache_vhosts` in config.yml)

## Author Information

This VM was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
