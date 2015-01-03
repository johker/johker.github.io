---
layout: post
title: "A Very Basic Octopress Setup Using Vagrant"
date: 2015-01-03 16:49:58 +0000
comments: true
categories: [Vagrant, Octopress, github]

---


Setting up Octopress can be tricky, especially on Windows systems. Using a Vagrant powered virtual machine instead we are only one command away from a blogging environment ready-to-go. Run from the directory of the Vagrantfile *vagrant up* will create a VirtualBox Image with Ubuntu 12.04 LTS.


``` ruby Vagrantfile for Octopress Setup https://github.com/johker/octopress_vagrant/blob/master/Vagrantfile Source Article
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	config.vm.box = "octopress" 

  	config.vm.box_url = "https://github.com/kraksoft/vagrant-box-ubuntu/releases/download/14.04/ubuntu-14.04-amd64.box"

  	config.vm.network :private_network, ip: "192.168.34.10"
  	
	config.vm.provider "virtualbox" do |v|
	    v.memory = 2048
	end
  
  	# Install octopress
	config.vm.provision :shell, :path => "scripts/octopress.sh"
  
  	# Sync posts folder  	
  	config.vm.synced_folder "posts/", "/opt/octopress/source/_posts/"
    
end
```