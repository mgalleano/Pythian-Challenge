# -*- mode: ruby -*-
# vi: set ft=ruby :

## Added by me:
require 'json'

$script = <<SCRIPT
echo " $(date) | $(curl -s -X GET 'http://checkip.dyndns.org/' | awk 'BEGIN { FS = "<|>" } ; { print $13 }')" >> /tmp/output.txt
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu14-cloudimage"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  # Your implementation goes here
  
  config.vm.network :forwarded_port, guest: 80, host: 8081
  config.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
        vb.gui = true
      # Customize the amount of memory on the VM:
        vb.memory = "1024"
  end
  
  config.vm.provision "chef_client" do |chef|
  # Add a recipe
  chef.add_recipe "apache2"
  chef.json = { :apache => { :default_site_enabled => true } }
  end

  # Adding requested script
  config.vm.provision "shell", inline: $script

end