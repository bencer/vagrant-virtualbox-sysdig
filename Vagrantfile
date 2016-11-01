# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant box with Docker, Docker Compose and Sysdig

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"
  config.vm.synced_folder ".", "/home/sysdig"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
    curl -s https://s3.amazonaws.com/download.draios.com/DRAIOS-GPG-KEY.public | sudo apt-key add -
    echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list
    curl -s /etc/apt/sources.list.d/draios.list | sudo tee http://download.draios.com/stable/deb/draios.list
    sudo apt-get update
    sudo apt-get install -y docker-engine linux-headers-$(uname -r) sysdig
    sudo usermod -aG docker ubuntu
    sudo service docker start
    curl -s -L "https://github.com/docker/compose/releases/download/1.8.1/docker-compose-$(uname -s)-$(uname -m)" | sudo tee /usr/local/bin/docker-compose > /dev/null
    sudo chmod 755 /usr/local/bin/docker-compose
    sudo apt-get clean
    sudo dd if=/dev/zero of=/EMPTY bs=1M
    sudo rm -f /EMPTY
  SHELL

end
