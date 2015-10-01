# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  # networking
  config.vm.network "private_network", ip: "192.168.25.25"
  config.vm.hostname = "xbmc-video-server"

  # memory usage
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
  end

  # synced folder
  config.vm.synced_folder "./", "/vagrant",
    owner: "vagrant",
    group: "www-data",
    mount_options: ["dmode=775,fmode=664"]

  # provisioning
  config.vm.provision "shell", path: "provisioning/01-configure-system.sh",
    name: "01 - Configure system"
  config.vm.provision "shell", path: "provisioning/02-install-system-packages.sh",
    name: "02 - Install and update system packages"
  config.vm.provision "shell", path: "provisioning/03-install-npm-dependencies.sh",
    name: "03 - Install npm dependencies"
  config.vm.provision "shell", path: "provisioning/04-configure-apache.sh",
    name: "04 - Configure Apache"
  config.vm.provision "shell", path: "provisioning/05-configure-xbmc-video-server.sh",
    name: "05 - Configure XBMC Video Server"

  # recurring provisioning
  config.vm.provision "shell", path: "provisioning/98-perform-post-update-tasks.sh", 
    name: "98 - Perform any post-update tasks",
    run: "always"
  config.vm.provision "shell", path: "provisioning/99-print-information.sh",
    name: "99 - Show information",
    run: "always"
end
