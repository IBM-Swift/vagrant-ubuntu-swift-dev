# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # Swift development targets Ubuntu 15.10
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.define "swift-dev" do |swiftdev|
  end

  config.vm.provider "virtualbox" do |vb|
    vb.name = "swift-dev"
    # Building swift requires significant resources
    vb.memory = "6144"
    vb.cpus = 4
  end

  # Prevents "stdin: is not a tty" on Ubuntu (https://github.com/mitchellh/vagrant/issues/1673)
  config.vm.provision "fix-no-tty", type: "shell" do |s|
    s.privileged = false
    s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
  end

  # Initialise development environment
  config.vm.provision "shell", inline: <<-SHELL
    echo "Updating virtual machine..."
    sudo DEBIAN_FRONTEND=noninteractive apt-get update

    echo "Installing swift prerequisites..."
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y git
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y cmake
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y ninja-build
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y clang
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y python
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y uuid-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libicu-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y icu-devtools
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libbsd-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libedit-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libxml2-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libsqlite3-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y swig
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libpython-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libncurses5-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y pkg-config
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y python-setuptools
    
    echo "Installing libdispatch prerequisites..."
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y autoconf
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libtool
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y pkg-config
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libblocksruntime-dev
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -y libbsd-dev

    echo "Installing Sphinx..."
    sudo easy_install -U Sphinx==1.3.4

    # Create development directory
    cd /vagrant && mkdir -p swift-dev && cd swift-dev

    echo "Cloning swift from GitHub..."
    if [ ! -d "swift" ]; then
      git clone https://github.com/apple/swift.git
    fi
    cd swift

    echo "Cloning swift subprojects from GitHub..."
    ./utils/update-checkout --clone

    echo "Finished setting up development environment - run 'vagrant ssh' to connect,"
    echo "then '/vagrant/swift-dev/swift/utils/build-script' to compile swift"
  SHELL
end
