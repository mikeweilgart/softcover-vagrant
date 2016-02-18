# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "puppetlabs/ubuntu-14.04-64-nocm"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

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

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL

sudo apt-get -y update

# Command below are mostly copied from
# http://blog.hostilefork.com/mobi-pdf-epub-softcover-ubuntu/
# I added the -y flag so apt-get will run noninteractively.
# Other changes as noted.

sudo apt-get -y install ruby
sudo apt-get -y install gems

sudo apt-get -y install g++
sudo apt-get -y install ruby-dev

sudo apt-get -y install libcurl3 libcurl3-gnutls libcurl4-openssl-dev
# This next line was added to handle the failure of nokogiri to install correctly.
sudo apt-get -y install patch

sudo gem install softcover --pre --no-ri --no-rdoc

# The rest of this script is optional.  The above is enough to build
# HTML and EPUB builds of a book.  The rest is necessary for PDFs et. al.

sudo apt-get -y install imagemagick
sudo apt-get -y install default-jre
sudo apt-get -y install inkscape
sudo apt-get -y install phantomjs
sudo apt-get -y install calibre
sudo apt-get -y install texlive-full

sudo apt-get -y install nodejs
cd /usr/local/bin
sudo ln -s /usr/bin/nodejs node

cd ~
wget https://github.com/IDPF/epubcheck/releases/download/v3.0/epubcheck-3.0.zip
unzip epubcheck-3.0.zip
rm epubcheck-3.0.zip
# Below line was added; was missing from web page.
sudo mv epubcheck-3.0 /usr/local/bin/

# This section is for kindlegen; you can comment it out if you don't want kindlegen.
cd ~
wget http://kindlegen.s3.amazonaws.com/kindlegen_linux_2.6_i386_v2_9.tar.gz
# The below lines were modified from the original commands on the website.
# Note that this doesn't install the docs for kindlegen; this section could be improved.
tar xf kindlegen_linux_2.6_i386_v2_9.tar.gz kindlegen
mv kindlegen /usr/local/bin/
rm kindlegen_linux_2.6_i386_v2_9.tar.gz

# Might as well be able to do asciidocs, also.
sudo apt-get -y install asciidoc

# See the README file included with this Vagrantfile for additional instructions,
# mostly taken from:
# https://scotch.io/tutorials/how-to-create-a-vagrant-base-box-from-an-existing-one
# Follow the instructions given in the README file
# to repackage your vagrant box, so you don't have to reprovision it
# each time you vagrant up - a lengthy process!
# Alternatively, you can just use vagrant halt instead of vagrant destroy,
# but you might as well repackage for maximum flexibility and recovery from any mistakes.
# Either way you will be storing the box on your computer.

   SHELL
end
