# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "phusion/ubuntu-14.04-amd64"
  config.vm.network "forwarded_port", guest: 2375, host: 2375
  config.vm.network "forwarded_port", guest:   80, host: 8080

  config.vm.provision :shell, inline: <<-SHELL
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
echo 'deb https://get.docker.io/ubuntu docker main' > /etc/apt/sources.list.d/docker.list

apt-get update
apt-get dist-upgrade -u -y
apt-get install -y lxc-docker
apt-get autoremove --purge -y

adduser vagrant docker

echo 'DOCKER_OPTS="-H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock"' >> /etc/default/docker
restart docker
  SHELL
end
