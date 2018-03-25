# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 4
  end

  config.vm.provision "shell", inline: <<-SHELL
    wget -O /etc/apt/sources.list https://repogen.simplylinux.ch/txt/xenial/sources_61bc792accfd6401d3eb9887e7398bab9fb724eb.txt    
    apt-get update
    apt-get upgrade -y
    apt-get install -y language-pack-ja
    update-locale LANG=ja_JP.UTF-8 
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
