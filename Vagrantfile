# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/xenial64"
  
  # Disable automatic box update checking. 
  config.vm.box_check_update = true
  
  # Forwarded port mapping
  # HTTP
  config.vm.network "forwarded_port", guest: 80, host: 80, uto_correct: true
  # HTTPS
  config.vm.network "forwarded_port", guest: 443, host: 443, auto_correct: true
  #  5900-5949: Spice viewer 
  for i in 5900..5949
    config.vm.network :forwarded_port, guest: i, host: i
  end
  #  55900-55949: web browser viewer 
  for i in 55900..55949
    config.vm.network :forwarded_port, guest: i, host: i
  end
  
  # map to sync folder to the currrent dir on the host machine
  config.vm.synced_folder ".", "/vagrant_data"
  
  # Virtualbox Provider-specific configuration
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
    
    # Customize the amount of memory on the VM:
    vb.memory = "4096"

    # Enabled nested hardware virtualization
    vb.customize ['modifyvm', :id, '--nested-hw-virt', 'on']
  end

  # Install docker-compose
  config.vm.provision "shell", inline: <<-SHELL
  curl -sL "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  chmod +x /usr/local/bin/docker-compose
  SHELL
  
  # Set up Docker provisioner in the new VM: https://www.vagrantup.com/docs/provisioning/docker
  config.vm.provision :docker

  # [Does not work] Requires vagrant-disksize plugin https://github.com/sprotheroe/vagrant-disksize
  config.disksize.size = '50GB'

end
