# Pre installed Noded Version
NODE_VERSION = "6.10"

# One to One mapping
# 3000 means forwarding host 3000 to guest 3000
OPEN_PORTS = 3000..3010

# Memory in MB
MEMORY = "8192"
VIDEO_MEMORY = "128"

# Number of cores
NUMBER_OF_CPUS = "4"


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
  # within the machine from a port on the host machine.
  # NOTE: This will enable public access to the opened port
  OPEN_PORTS.each do |i|
    config.vm.network "forwarded_port", guest: i, host: i
  end

  config.vm.provider "virtualbox" do |vb|
    vb.memory = MEMORY
    vb.cpus = NUMBER_OF_CPUS
    vb.customize ["modifyvm", :id, "--vram", VIDEO_MEMORY]
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
  end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo apt-get update

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
    sudo apt install -y code
    code --install-extension ms-vsliveshare.vsliveshare
    code --install-extension equinusocio.vsc-material-theme
    code --install-extension dbaeumer.vscode-eslint
    code --install-extension ms-vscode.vscode-typescript-tslint-plugin
    wget -oq- https://raw.githubusercontent.com/rsferreira11/vscode-settings/master/settings.json -P /home/vagrant/.config/Code/User/

    sudo wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
    echo "source /home/vagrant/.nvm/nvm.sh" >> /home/vagrant/.profile
    source /home/vagrant/.profile
    nvm install #{NODE_VERSION}

    sudo apt-get install -y gparted
    mkdir /home/vagrant/games
  SHELL
end
