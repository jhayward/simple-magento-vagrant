# -*- mode: ruby -*-
# vi: set ft=ruby :

# To install store sample data
sample_data = "true"

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"

   #virtualbox specific
  config.vm.provider :virtualbox do |vb, override|
    override.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777","fmode=666"]
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant", "1"]
    vb.name = "simple-magento-vagrant"
  end

  config.vm.provider "parallels" do |v, override|
    override.vm.box = "parallels/ubuntu-14.04"
    override.vm.box_url = "https://vagrantcloud.com/parallels/ubuntu-14.04"
  end  
  
  config.vm.provision :shell, :path => "bootstrap.sh", :args => [sample_data]

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network :forwarded_port, guest: 80, host: 8080
  
  config.vm.provider "parallels" do |v, override|
    override.vm.synced_folder ".", "/vagrant", mount_options: ["share", "nosuid"]
  end

  config.ssh.forward_agent = true
end
