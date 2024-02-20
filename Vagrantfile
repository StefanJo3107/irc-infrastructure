# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "generic/debian12"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = "qemu"
    libvirt.memory = 256
  end

  config.vm.define "irc" do |irc|
    app.vm.hostname = "badusb-irc.test"
    app.vm.network :private_network, ip: "192.168.60.4"
  end

  config.vm.define "db1" do |app|
    app.vm.hostname = "badusb-db1.test"
    app.vm.network :private_network, ip: "192.168.60.5"
  end

  config.vm.define "db2" do |app|
    app.vm.hostname = "badusb-db2.test"
    app.vm.network :private_network, ip: "192.168.60.6"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "configure.yml"
  end
end
