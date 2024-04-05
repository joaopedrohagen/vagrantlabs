# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure("2") do |config|
  (1..2).each do |i|
    config.vm.define "SRV00#{i}" do |srv|
      srv.vm.box = "ubuntu/trusty64"
      srv.vm.hostname = "SRV00#{i}"
      srv.vm.network "private_network", bridge: 'eth0', ip: "192.168.56.24#{i}"
      srv.vm.allow_fstab_modification = true
      srv.ssh.forward_x11 = true
      # Uncomment this part for resize the disk.
      # If the disk has a default size, it won't work
      # Run this command before: vagrant plugin install vagrant-disksize
      srv.disksize.size = '10GB'

      srv.vm.provider :virtualbox do |v|
        v.name = "SRV00#{i}"
        v.cpus = 1
        v.memory = 1024
      end

      srv.vm.provision "shell", inline: <<-SHELL
        sudo apt-get update -y
        sudo apt-get upgrade -y
      SHELL
    end
  end
end
