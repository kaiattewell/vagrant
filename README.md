# Kais first vagrantfile 

Template file for booting VMS using vagrant and a YAML file for configuration

## Defining new machines

New machines are defined in the YAML file "info.yml" 
The guest name, box, cpus, memory,ip and port must be defined(port is for running python program preinstalled on VM)


    -name: jenkins
     box: centos/7
     cpus: 1
     memory: 4096 
     ip: 192.168.33.11
     port: 8001
    

## Required
name:
The name is how you can interact with the guest via Vagrant, for example to only start the virtual machine called default you could run vagrant up default

box:
The name of the box to be provisioned on the guest machine that is either installed locally or downloaded from the Vagrant Cloud

cpus:
Amount of cpus to assign to the guest machine

memory:
Amount of RAM in Megabytes to assign to the guest machine

ip:
Private IP address of the guest machine, which will allow connectivity from the host

port:
the port number the python program is forwarded to in order to allow access from other machines

## Optional
Package manager:
The option to set the package manager of the OS in order to correctly install packagaes listed in the below option

Packages:
Optional packaages to be installed upon creation of the virtual machine

