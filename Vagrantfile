# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/bionic64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 3001, host: 3001
  config.vm.network "forwarded_port", guest: 3002, host: 3002
  config.vm.network "forwarded_port", guest: 3003, host: 3003
  config.vm.network "forwarded_port", guest: 3004, host: 3004
  config.vm.network "forwarded_port", guest: 3005, host: 3005
  config.vm.network "forwarded_port", guest: 3006, host: 3006
  config.vm.network "forwarded_port", guest: 3006, host: 3006
  config.vm.network "forwarded_port", guest: 3007, host: 3007
  config.vm.network "forwarded_port", guest: 3008, host: 3008
  config.vm.network "forwarded_port", guest: 3009, host: 3009
  config.vm.network "forwarded_port", guest: 3010, host: 3010

  config.vm.provider "virtualbox" do |vb| 
    # Customize the amount of memory on the VM:
    vb.memory = "8192"

    # Number of CPUs
    vb.cpus = "4"

    # Video Memory
    vb.customize ["modifyvm", :id, "--vram", "128"]
  end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y curl
    
    sudo apt-get install -y virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11
    sudo VBoxClient --clipboard
    sudo VBoxClient --draganddrop
    sudo VBoxClient --display
    sudo VBoxClient --checkhostversion
    sudo VBoxClient --seamless

    sudo apt-get install -y --no-install-recommends ubuntu-desktop

    sudo apt-get install -y firefox

    sudo wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
    sudo apt install code
    code --install-extension ms-vsliveshare.vsliveshare
    code --install-extension equinusocio.vsc-material-theme
    code --install-extension dbaeumer.vscode-eslint
    code --install-extension ms-vscode.vscode-typescript-tslint-plugin
    
    sudo wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
    command -v nvm
    nvm install 6.10
  SHELL
end
