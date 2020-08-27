# burnsyvagrantfiles

quick jenkins on ubuntu bionic64

# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$script = <<ENDSCRIPT
 wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
 sudo apt-add-repository "deb http://pkg.jenkins-ci.org/debian binary/"
 sudo apt-get install jenkins  sudo systemctl start jenkins.service
 sudo systemctl enable jenkins.service
ENDSCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.network "forwarded_port", guest: 8080, host: 8888
  config.vm.provision "shell", inline: $script
end
