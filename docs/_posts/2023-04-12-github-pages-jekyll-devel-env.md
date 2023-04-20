---
layout: single
title: "Quick start for GitHub Pages using Vagrant (II)"
date: 2023-04-12 10:12:00 +0000
last_modified_at: 2023-04-19 09:48:00 +0000
categories: quick-start github-pages jekyll devel-env vagrant
---

## Setting up the development environment from scratch 

### Prerequisite

* `Vagrant` is installed. See ["Vagrant Tutorial - Install Vagrant"](https://developer.hashicorp.com/vagrant/tutorials/getting-started/getting-started-install) or ["Vagrant Document - Install Vagrant"](https://developer.hashicorp.com/vagrant/docs/installation) for more details on how to install `Vagrant`.
* Any virtualization product (e.g., `VirtualBox`) is installed. See ["VirtualBox User Manual - Chapter 2. Installation Details"](https://www.virtualbox.org/manual/ch02.html) for more details on how to install `VirtualBox`.

### Creating Ubuntu-22.04 machine using Vagrant

1. Create a new directory for your vagrant box and move to the directory.

   ```
   $ mkdir <vagrant box name>
   $ cd <vagrant box name>
   ```

2. Initialize a Vagrant box for Ubuntu-22.04 in the directory.

   ```
   $ vagrant init bento/ubuntu-22.04
   $ vagrant up
   ```

   NOTE: You can find other Vagrant boxes from ["HashiCorp's Vagrant Cloud box catalog"](https://app.vagrantup.com/boxes/search).

   NOTE: `vagrant init` command creates an initial `Vagrantfile` and initializes the current directory for Vagrant environment. See ["Vagrant Document - Commands (CLI) > Init"](https://developer.hashicorp.com/vagrant/docs/cli/init) for more details.

   NOTE: `vagrant up` command creates a new guest machine based on `Vagrantfile`. See ["Vagrant Document - Commands (CLI) > Up"](https://developer.hashicorp.com/vagrant/docs/cli/up).

   NOTE: Before executing `vagrant up` command, `Vagrantfile` can be manually configured for your project. See ["Vagrant Document - Vagrantfile"](https://developer.hashicorp.com/vagrant/docs/vagrantfile).

### Installing Jekyll on Ubuntu-22.04 guest machine

1. Connect to the new guest machine using `vagrant ssh` command.

   ```
   $ vagrant ssh
   Welcome to Ubuntu 22.04 LTS (GNU/Linux 5.15.0-30-generic x86_64)

    * Documentation:  https://help.ubuntu.com
    * Management:     https://landscape.canonical.com
    * Support:        https://ubuntu.com/advantage

     System information as of Thu Mar  2 10:00:12 PM UTC 2023

     System load:  0.12744140625      Processes:             115
     Usage of /:   15.6% of 30.34GB   Users logged in:       1
     Memory usage: 36%                IPv4 address for eth0: 10.0.2.15
     Swap usage:   0%

   This system is built by the Bento project by Chef Software
   More information can be found at https://github.com/chef/bento
   Last login: Thu Mar  2 21:00:30 2023 from 10.0.2.2
   vagrant@vagrant:~$
   ```

   NOTE: See ["Vagrant Document - Commands (CLI) > SSH"](https://developer.hashicorp.com/vagrant/docs/cli/ssh) for more details.

   NOTE: PuTTY can be used for connecting to the vagrant guest machine as an alternative to `vagrant ssh` command. See ["PuTTY as an alternative to `vagrant ssh`"]({% link _posts/2023-04-19-vagrant-ssh-alternative-putty.md %}).

2. Install Jekyll and its dependencies.

   ```
   $ sudo apt-get update
   $ sudo apt-get install ruby-full build-essential zlib1g-dev

   $ echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
   $ echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
   $ echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
   $ source ~/.bashrc

   $ gem install jekyll bundler
   ```

   NOTE: See ["Jekyll Docs - Jekyll on Ubuntu"](https://jekyllrb.com/docs/installation/ubuntu/) for more details.


## Setting up the development environment using pre-configured `Vagrantfile` 

### Prerequisite

* `Vagrant` is installed. See ["Vagrant Tutorial - Install Vagrant"](https://developer.hashicorp.com/vagrant/tutorials/getting-started/getting-started-install) or ["Vagrant Document - Install Vagrant"](https://developer.hashicorp.com/vagrant/docs/installation) for more details on how to install `Vagrant`.
* Any virtualization product (e.g., `VirtualBox`) is installed. See ["VirtualBox User Manual - Chapter 2. Installation Details"](https://www.virtualbox.org/manual/ch02.html) for more details on how to install `VirtualBox`.

### How-To

1. Create a new directory for your vagrant box and move to the directory.

   ```
   $ mkdir <vagrant box name>
   $ cd <vagrant box name>
   ```

2. Download the pre-configured [`Vagrantfile`](https://github.com/74luftikus/74luftikus.github.io/blob/main/resources/vagrant/ubuntu22.04/Vagrantfile) and put it to the current directory.

3. Create a new Ubuntu 22.04 guest machine using the pre-configured `Vagrantfile` by executing the following:

   ```
   $ vagrant up
   ```

   NOTE: Before executing `vagrant up` command, `Vagrantfile` can be additionally modified for your project if required. See ["Vagrant Document - Vagrantfile"](https://developer.hashicorp.com/vagrant/docs/vagrantfile).

   NOTE: By default, the following port forwarding mapping is configured for Jekyll server. Please change it properly according to your environment.

   ```
   config.vm.network "forwarded_port", guest: 4000, host: 4000
   ```

   NOTE: By default, the following shared folder mapping is configured for my own directory structure. Please change it properly according to your directory structure.

   ```
   config.vm.synced_folder "../projects", "/projects"
   ```

   NOTE: By default, the following provision is configured, which automatically installs Jekyll and its dependencies as described in ["Jekyll Docs - Jekyll on Ubuntu"](https://jekyllrb.com/docs/installation/ubuntu/).

   ```
      config.vm.provision "shell", privileged: false, inline: <<-SHELL
      sudo apt-get update
      sudo apt-get -y install ruby-full build-essential zlib1g-dev
      export GEM_HOME="$HOME/gems"
      export PATH="$HOME/gems/bin:$PATH"
      gem install jekyll bundler
      echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
      echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
      echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
      gem install jekyll bundler
    SHELL
   ```

## References

* [Vagrant Documentation](https://developer.hashicorp.com/vagrant/docs)
* [VirtualBox Documentation](https://www.virtualbox.org/wiki/Documentation) 
* [Jekyll Docs - Installation](https://jekyllrb.com/docs/installation/)
