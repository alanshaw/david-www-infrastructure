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

  # Common config
  config.vm.box = "ubuntu/trusty64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  # Setup the primary "app", that'll be the prod system.
  config.vm.define "app", primary: true do |app|
    app.vm.hostname = "dev.david-dm.org"
    app.vm.network "private_network", ip: "10.211.55.6"
    app.vm.provision "ansible" do |ansible|
      ansible.inventory_path = "provision/dev"
      ansible.playbook = "provision/playbook.yml"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_user: "vagrant"
      }
      ansible.verbose = "v"
    end
  end

end
