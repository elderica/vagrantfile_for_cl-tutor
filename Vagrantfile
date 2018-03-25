# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.box = "ubuntu/xenial64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    #  vb.gui = true
 
    vb.memory = "4096"
    vb.cpus = 4
  end

  config.vm.provision "shell", inline: <<-SHELL
    wget -O /etc/apt/sources.list https://repogen.simplylinux.ch/txt/xenial/sources_61bc792accfd6401d3eb9887e7398bab9fb724eb.txt    
    apt-get update
    apt-get upgrade -y
    apt-get install -y language-pack-ja
    update-locale LANG=ja_JP.UTF-8 
    #wget -O /tmp/ros.deb https://github.com/roswell/roswell/releases/download/v18.3.10.89/roswell_18.3.10.89-1_amd64.deb
    #dpkg -i /tmp/ros.deb
    apt install -y git build-essential automake libcurl4-openssl-dev libncursesw5-dev libncurses5-dev git
    cd /tmp && sudo -u vagrant -i git clone https://github.com/roswell/roswell.git /tmp/roswell
    cd /tmp/roswell && sudo -u vagrant sh bootstrap
    cd /tmp/roswell && sudo -u vagrant ./configure
    cd /tmp/roswell && sudo -u vagrant make
    cd /tmp/roswell && make install
    sudo -u vagrant -i ros
    sudo -u vagrant -i ros install cxxxr/lem
    sudo -u vagrant -i ros install t-cool/cl-tutor
    sudo -u vagrant -i echo -e "export PATH=\$\{PATH\}:~vagrant/.roswell/bin" >> ~vagrant/.profile
  SHELL
end
