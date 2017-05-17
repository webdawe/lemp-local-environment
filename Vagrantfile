# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

VM_IP = '192.168.1.206'
VM_BOX = 'ubuntu/trusty64'
VM_CODE_SOURCE = '/home/anil/sites/'
VM_CODE_DESTINATION = '/var/www/'

PRIVATE_KEY_SOURCE      = '/home/anil/vm/files/ssh/vagrant/vagrant.pub'
PRIVATE_KEY_DESTINATION = '/home/vagrant/.ssh/id_rsa'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box =VM_BOX
   
  #public network Accessable from machines in the local network	 
  config.vm.network :public_network, ip: VM_IP #, bridge: "en1: Wi-Fi (AirPort)"

  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'" # avoids 'stdin: is not a tty' error.
  config.ssh.forward_agent = true   

  

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, '--chipset', 'ich9']
    v.customize ["modifyvm", :id, "--name", "Webdawe-Development"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", 4096] #4GB memory
    v.customize ["modifyvm", :id, "--ioapic", "on"] 
    v.gui = false
    v.cpus = 2
  end 

  #666 otherwise ansible fails on the host files
  config.vm.synced_folder '.', '/vagrant', mount_options: ["dmode=666","fmode=666"]
  
  #code source for websites
  config.vm.synced_folder VM_CODE_SOURCE, VM_CODE_DESTINATION, owner: "www-data", group: "www-data"

  config.vm.provision :shell, :path => "shell/ansible-install.sh"
  config.vm.provision :shell, :path => "shell/ansible-run.sh"
end

      