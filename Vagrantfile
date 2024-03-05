# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "generic/debian12"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = "qemu"
    libvirt.memory = 2048
  end

  config.vm.define "irc" do |irc|
    irc.vm.hostname = "badusb-irc.test"
    irc.vm.network :private_network, ip: "192.168.60.4"
    irc.vm.network "forwarded_port", guest: 6697, host: 6697
    irc.vm.network "forwarded_port", guest: 6667, host: 6667
    irc.vm.provision "ansible" do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "configure.yml"
      ansible.inventory_path = "inventories/vagrant/inventory"
      ansible.compatibility_mode = "2.0"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_user: "vagrant",
        ansible_ssh_private_key_file: "../../vagrant/insecure_private_key"
      }
    end
  end

  config.vm.define "db1" do |db|
    db.vm.hostname = "badusb-db1.test"
    db.vm.network :private_network, ip: "192.168.60.5"
  end

  config.vm.define "db2" do |db|
    db.vm.hostname = "badusb-db2.test"
    db.vm.network :private_network, ip: "192.168.60.6"
  end

  config.vm.define "payload_server" do |ps|
    ps.vm.hostname = "badusb-payload.test"
    ps.vm.network :private_network, ip: "192.168.60.7"
    ps.vm.network "forwarded_port", guest: 80, host: 3000
  end
end
