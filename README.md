# Acquia Cloud VM

I use this VM to test things in an environment close to that of Acquia's Cloud servers, following the guide at [Acquia Cloud technology platform and supported software](https://docs.acquia.com/cloud/arch/tech-platform).

Includes (or will soon include):

  - Apache 2.2.22
  - MySQL 5.5.x
  - PHP 5.3.x (5.5.x configurable)
  - Varnish 3.x
  - Memcached 1.4.x
  - Drush 6.x
  - Git
  - etc.

## Usage

  1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads), [Vagrant](https://www.vagrantup.com/downloads.html), and [Ansible](http://docs.ansible.com/intro_installation.html):
    - `$ brew cask install virtualbox vagrant`
    - `$ brew install ansible`
  2. (From the same directory as this README file) run `$ vagrant up`

*This assumes you have [Homebrew](http://brew.sh/) installed and have `cask` installed (`brew tap caskroom/cask && brew install brew-cask` to install).*

## Author Information

This VM was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
