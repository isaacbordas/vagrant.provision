Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.network "private_network", ip: "192.168.33.177"

  config.vm.synced_folder "web", "/var/www"

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    echo "Updating source list" | tee /home/ubuntu/vm_build.log
    apt-get update >> /home/ubuntu/vm_build.log
    echo "Installing apache2" | tee /home/ubuntu/vm_build.log
    apt-get install -y apache2 >> /home/ubuntu/vm_build.log
    echo "Installing ondrej repo" | tee /home/ubuntu/vm_build.log
    apt-get install -y software-software-properties >> /home/ubuntu/vm_build.log
    add-apt-repository -y ppa:ondrej/php >> /home/ubuntu/vm_build.log
    echo "Updating source list" | tee /home/ubuntu/vm_build.log
    apt-get update -y >> /home/ubuntu/vm_build.log
    echo "Installing php7.2" | tee /home/ubuntu/vm_build.log
    apt-get install -y php7.2 libapache2-mod-php7.2 php7.2-curl php7.2-json php7.2-cli php7.2-common php7.2-mbstring php7.2-gd php7.2-intl php7.2-xml php7.2-mysql php7.2-zip >> /home/ubuntu/vm_build.log
    echo "Installing mysql" | tee /home/ubuntu/vm_build.log
    debconf-set-selections <<< 'mysql-server mysql-server/root_password password your_password'
    debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password your_password'
    apt-get install -y mysql-server >> /home/ubuntu/vm_build.log
    echo "Restart apache2" | tee /home/ubuntu/vm_build.log
    service apache2 restart >> /home/ubuntu/vm_build.log
    echo "Installing composer" | tee /home/ubuntu/vm_build.log
    curl --silent https://getcomposer.org/installer | php >> /home/ubuntu/vm_build.log
    mv composer.phar /usr/local/bin/composer >> /home/ubuntu/vm_build.log
    echo "Installing git" | tee /home/ubuntu/vm_build.log
    apt-get install -y git >> /home/ubuntu/vm_build.log
    echo "Creating 2Gb swap" | tee /home/ubuntu/vm_build.log
    fallocate -l 2G /swapfile
    chmod 600 /swapfile
    mkswap /swapfile
    swapon /swapfile
    echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
    echo "Enable mod_rewrite" | tee /home/ubuntu/vm_build.log
    sudo a2enmod rewrite >> /home/ubuntu/vm_build.log
  SHELL
end
