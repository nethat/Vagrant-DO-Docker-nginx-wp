# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

    config.vm.network "forwarded_port", guest: 80, host: 8080
    config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = '~/.ssh/id3_rsa'
    override.vm.box = 'digital_ocean'
#   override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"
    provider.token = '52215514298b73f9b55fcbc8f03b448f3162cd2d43ed6844bde2cbc58fa8b6ca'
    provider.image = 'ubuntu-14-04-x64'
    provider.region = 'nyc2'
    provider.size = '512mb'

    config.vm.provision "shell", inline: <<-SHELL
     unset UCF_FORCE_CONFFOLD
     export UCF_FORCE_CONFFNEW=YES
     ucf --purge /boot/grub/menu.lst
     export DEBIAN_FRONTEND=noninteractive
     apt-get update
     apt-get -o Dpkg::Options::="--force-confnew" --force-yes -fuy dist-upgrade 
     sudo apt-get install -y ufw
     sudo apt-get install -y fail2ban
     sudo apt-get install -y curl
     apt-get install -y software-properties-common git
     curl -sSL https://get.docker.com/ubuntu/ | sudo sh
git clone https://github.com/eugeneware/docker-wordpress-nginx.git
cd docker-wordpress-nginx
sudo docker build -t="docker-wordpress-nginx" .
   SHELL
   end
end
