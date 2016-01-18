# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :web do |web_config|
      web_config.vm.box = "../../vagrant/precise32"
      web_config.vm.network :private_network, ip: "192.168.33.10"
      web_config.ssh.private_key_path = "~/.ssh/id_rsa"
      # web_config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
      web_config.vm.provision "shell", inline: "cat ~/.ssh/id_rsa.pub >> ~vagrant/.ssh/authorized_keys"
      web_config.ssh.forward_agent = true

      web_config.vm.provision :ansible do |ansible|
          ansible.playbook = "devops/webserver.yml"
          ansible.inventory_path = "devops/inventory"
          ansible.limit = "webserver"
      end
  end

  config.vm.define :db do |db_config|
      db_config.vm.box = "../../vagrant/precise32"
      db_config.vm.network :private_network, ip: "192.168.33.20"
      db_config.ssh.private_key_path = "~/.ssh/id_rsa"
      # db_config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
      db_config.vm.provision "shell", inline: "cat ~/.ssh/id_rsa.pub >> ~vagrant/.ssh/authorized_keys"
      db_config.ssh.forward_agent = true

      db_config.vm.provision :ansible do |ansible|
          ansible.playbook = "devops/dbserver.yml"
          ansible.inventory_path = "devops/inventory"
          ansible.limit = "dbserver"
      end
  end
end
