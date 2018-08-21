# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

#requires
require 'yaml'
require 'json'
require 'rubygems'

filename = "info"

if File.file? "#{filename}.json"
    info = JSON.parse(File.read("#{filename}.json"))
else
    info = YAML.load_file("#{filename}.yaml")
end



Vagrant.configure("2") do |config|

	info.each do |info|
		config.vm.define info['name'] do |info_vm|
			set_box(info, info_vm)
			set_cpu_mem(info, info_vm)
			set_ip(info, info_vm)
			#set_port_fwd(info, info_vm)
			#sharefol(info, info_vm)
			#info_vm.vm.provision "shell", path:"vagrantscripts/installscript"

		end
	end
end
		
# sets the memory and amount of cores from the YAML
def set_cpu_mem(info, info_vm)
	info_vm.vm.provider "virtualbox" do |vb|	
		vb.cpus = info['cpus']
		vb.memory = info['memory']
	end
end

#Sets the box type from the YAML
def set_box(info, info_vm)
	info_vm.vm.box = info['box']
end

#Sets the IP of each VM from the YAML
def set_ip(info, info_vm)
	info_vm.vm.network "private_network", ip: info['ip']
end

#sets the port to forward for HTTP program using the YAML
def set_port_fwd(info, info_vm)
	 info_vm.vm.network "forwarded_port", guest: 9000, host: info['port']
end

#script to install packages for android or regular package managers
def install_package(info, info_vm)
	unless info['packages'].nil?
		if info['package_manager'] == "apk"
			info_vm.vm.provision "shell", inline: <<-SHELL
				sudo #{info['package_manager']} install #{info['packages'].join(" ")}
			SHELL
		else
			info_vm.vm.provision "shell", inline: <<-SHELL
				sudo #{info['package_manager']} install -y #{info['packages'].join(" ")}
			SHELL
		end
	end
end

# possibly create shared folders for the VMS WORK IN PROGRESS
def sharefol(info, info_vm)
		info_vm.vm.synced_folder info['OSshare'], info['VMshare']
end
		
			

  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  #config.vm.define "jenkins" do |jenkins|
  #jenkins.vm.box = "centos/7"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
 # jenkins.vm.network "forwarded_port", guest: 9000, host: 8180

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
 # jenkins.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # jenkins.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
   #  vb.memory = "2048"
	# vb.cpus = "2"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # jenkins.vm.provision "shell", path:"vagrantscripts/installscript"

 #   apt-get install -y apache2
   
#end
#config.vm.define "server" do |server|
 # server.vm.box = "centos/7"
 # server.vm.provider "virtualbox" do |vb|
    # vb.memory = "2048"
	# vb.cpus = "2"
  # end
   #   server.vm.provision "shell", path:"vagrantscripts/installscript"
  # end

