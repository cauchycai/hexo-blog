---
title: "Install Ruby on Rails on Debian 7.5"
tags: [om, linux, ruby]
---
### Installing Passenger and Dependencies

	$ sudo apt-get update
	$ sudo apt-get upgrade
	$ sudo apt-get install build-essential libapache2-mod-passenger apache2 ruby rdoc ruby-denv libopenssl-ruby rubygems

### Using the gem package manager for Ruby modules, install the fastthread gem:

	$ sudo gem install fastthread
	$ sudo gem install rails

### Or install previous versions of rails

	$ gem install rails --version 2.1.2
	$ gem install rails --version 2.2.2
	$ gem install rails --version 2.3.5
	$ gem install rails --version 3.0.4

### Install RVM

	$ curl -L https://get.rvm.io | bash -s stable --ruby
	$ echo "source $HOME/.rvm/scripts/rvm" >> ~/.profile

