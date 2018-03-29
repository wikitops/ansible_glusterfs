# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"

  # Glsuter Server
  (1..2).each do |i|
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    config.vm.define "gfsserver0#{i}" do |server|
      server.vm.hostname = "gfsserver0#{i}"
      server.vm.network "private_network", ip: "10.0.3.6#{i}"
    end
  end

  # Glsuter Client
  (1..1).each do |i|
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    config.vm.define "gfsclient0#{i}" do |server|
      server.vm.hostname = "gfsclient0#{i}"
      server.vm.network "private_network", ip: "10.0.3.7#{i}"
    end
  end

  # Provision
  config.vm.provision "shell", path: "provision.sh"
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/authorized_keys"

end
