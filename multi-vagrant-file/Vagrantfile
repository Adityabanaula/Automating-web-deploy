Vagrant.configure("2") do |config|
   config.vm.define "ansible" do |ab|
   	ab.vm.box = "ubuntu/bionic64"
	ab.vm.network "private_network", ip: "192.168.33.15"
	ab.vm.network "public_network"
	ab.vm.provider "virtualbox" do |vb|
  		vb.memory = "1024"
   	end
	ab.vm.synced_folder "./ansible-files", "/vagrant_data"
	ab.vm.provision "shell", inline: <<-SHELL
      	#!/bin/bash
		sudo apt update -y
		sudo apt install software-properties-common
		sudo add-apt-repository --yes --update ppa:ansible/ansible
		sudo apt install ansible -y
   	SHELL
   end
   config.vm.define "web" do |web|
	web.vm.box = "geerlingguy/centos7"
	web.vm.network "private_network", ip: "192.168.33.16"
	web.vm.network "public_network"
	web.vm.provider "virtualbox" do |vb|
  		vb.memory = "1024"
   	end
   end
   config.vm.define "db" do |db|
	db.vm.box = "geerlingguy/centos7"
	db.vm.network "private_network", ip: "192.168.33.17"
	db.vm.network "public_network"
	db.vm.provider "virtualbox" do |vb|
  		vb.memory = "1024"
   	end
   end
end
