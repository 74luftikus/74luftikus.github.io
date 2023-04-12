---
layout: single
title: "Quick start for GitHub Pages using Vagrant"
date: 2023-04-11 18:48:00 +0000
categories: jekyll github-pages vagrant
---

## Creating a GitHub account

### How-To

It is quite easy to create a GitHub account. Just follow as described in ["GitHub Docs - Getting started with your GitHub account"](https://docs.github.com/en/get-started/onboarding/getting-started-with-your-github-account).

If you are not familiar with GitHub, then start from ["GitHub Skills"](https://skills.github.com/).

### References

* [GitHub Docs - Get started](https://docs.github.com/en/get-started)


## Creating a GitHub Pages site

### How-To

Similar to creating a GitHub account, it is also quite easy. Just follow as described in ["GitHub Docs - Quickstart for GitHub Pages"](https://docs.github.com/en/pages/quickstart) or ["Creating a GitHub Pages site"](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

NOTE: In case of GitHub free account, the repository for GitHub Pages must be set to **"public"**.

NOTE: The repository name for GitHub Pages must be **`<username>.github.io`**, which makes your GitHub Pages available at `https://<username>.github.io/`.

NOTE: After creating a new repository for GitHub Pages, it takes quite some time to publish your site. GitHub Docs says it can take up to 10 minutes, but it seems it takes more than 10 minutes. Maybe it happens only to me. :)

### References

* [GitHub Docs - GitHub Pages](https://docs.github.com/en/pages)
* [GitHub Skills - GitHub Pages](https://github.com/skills/github-pages)


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

### References

* [Vagrant Documentation](https://developer.hashicorp.com/vagrant/docs)
* [VirtualBox Documentation](https://www.virtualbox.org/wiki/Documentation) 
* [Jekyll Docs - Installation](https://jekyllrb.com/docs/installation/)


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

### References

* [Vagrant Documentation](https://developer.hashicorp.com/vagrant/docs)
* [VirtualBox Documentation](https://www.virtualbox.org/wiki/Documentation) 
* [Jekyll Docs - Installation](https://jekyllrb.com/docs/installation/)

## Creating a new Jekyll site on the Ubuntu guest machine

### Prerequisite

* A development environment is already set up as described above, and working without any problem.

### Creating a new Jekyll site using Jekyll's default theme `minima`

1. Create a new directory for your new Jekyll site and move to the directory.

   ```
   $ mkdir <site name>
   $ cd <site name>
   ```

2. Create a new Jekyll site by executing the following:

   ```
   $ jekyll new --skip-bundle .
   ```

   NOTE: This command generates the followings:

   ```
   .
   ├── 404.html
   ├── about.markdown
   ├── _config.yml
   ├── Gemfile
   ├── .gitignore
   ├── index.markdown
   └── _posts
       └── 2023-03-05-welcome-to-jekyll.markdown
   ```

   NOTE: In order to make it run on GitHub Pages, `Gemfile` and `_config.yml` file need to be edited. See ["GitHub Docs - Creating a GitHub Pages site with Jekyll > Creating your site"](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site) for more details.


3. Add a new page and post according to ["Jekyll Docs - Pages"](https://jekyllrb.com/docs/pages/) and ["Jekyll Docs - Posts"](https://jekyllrb.com/docs/posts/).

   NOTE: Depending on Jekyll theme you use, there might be slightly differences. Please check documents of Jekyll theme you use.

### Local deployment

1. Locally deploying the new Jekyll site for testing by executing the following:

   ```
   $ bundle exec jekyll serve --host 0.0.0.0
   ```

   NOTE: The current development environment is set up on the vagrant Ubuntu guest machine. This means your new Jekyll site is running on your guest machine, but your browser might be running on the host machine. For this reason, Jekyll needs an additional option "`--host 0.0.0.0`" which allows Jekyll server to receive requests from any of system interfaces. Without this option, Jekyll server accepts requests ONLY from `localhost`.

   NOTE: If you encounter "`cannot load such file -- webrick (LoadError)`" error, then add the below into `Gemfile` to resolve the issue.

   ```
   # Added to resolve an issue:
   # https://github.com/jekyll/jekyll/issues/8523
   gem "webrick"
   ```

   NOTE: If you encounter a warning message "`GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.`", then add the below into `_config.yml` to resolve this issue. See ["GitHub Pages Ruby Gem - Issue #399"](https://github.com/github/pages-gem/issues/399) for more details.

   ```
   # Added to resolve an issue:
   # https://github.com/github/pages-gem/issues/399
   github: [metadata]
   ```

2. Now your new Jekyll site is accessible at `http://localhost:4000`.

### References

* [Jekyll Docs - Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
* [Jekyll Docs - Configuration Options](https://jekyllrb.com/docs/configuration/options/#build-command-options)
* [Jekyll minima Theme](https://github.com/jekyll/minima)

