# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

version="3_0_4"

script = <<SCRIPT

apt-get update -y
apt-get install -y git autotools-dev libgdbm-dev libpcap-dev libsqlite3-dev dpkg-dev debhelper quilt libcurl4-openssl-dev libiodbc2-dev libjson-c-dev libjson0-dev libkrb5-dev libldap2-dev libpam0g-dev libperl-dev libmysqlclient-dev libpq-dev libreadline-dev libsasl2-dev libtalloc-dev libyubikey-dev python-dev

mkdir freeradius
cd freeradius

wget https://github.com/FreeRADIUS/freeradius-server/archive/release_#{version}.tar.gz

tar zxf release_#{version}.tar.gz
cd freeradius-server-release_#{version}/

fakeroot dpkg-buildpackage -b -uc

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = 'ubuntu/trusty64'

  config.vm.network :private_network, ip: "192.168.0.23"
  config.vm.network :forwarded_port, guest: 8000, host: 8000
  
  config.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", 2048,  "--cpus", "2"]
  end

  config.vm.provision :shell, inline: script 

end
