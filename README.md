# vagrant.provision
Provisioning vagrant box ubuntu/xenial64

This Vagrant script creates a Ubuntu's 64bit 16.04 LTS (ubuntu/xenial64) machine and provide it with a LAMP enviorement with the next actions:

- Install lastest Apache
- Adds ondrej's repository for the PHP 7
- Installs PHP 7.2
- Installs latest MySQL indicating the root password on the process
- Installs composer and makes it global
- Installs Git

Change the default password for the MySQL root user located in the Vagrantfile 
The local IP for this machine is 192.168.33.177. Change it for your convenience.
The synced_folder is web (relative on the Vagrantfile location) -> /var/www (default DocumentRoot folder for apache)
