# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box_check_update = false
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.ssh.insert_key = true

  config.vm.box = "vagrant-sandbox"
  config.vm.box_url = "https://artifactory-qa.bmogc.net/artifactory/api/vagrant/Devops_Vagrant/vagrant-sandbox"
  config.vm.box_download_insecure = true
  config.vm.box_version = ">= 2.0.5"

  config.vm.synced_folder "tools", "/home/vagrant/tools"

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  # Sets up two VMs based on this config

  config.vm.define "ctrlvm", primary: true do |ctrlvm|
    ctrlvm.vm.synced_folder "ctrl_share", "/home/vagrant/share", disabled: false, create: true
    ctrlvm.vm.hostname = "ctrlvm"
    ctrlvm.vm.network :private_network, ip: "172.28.128.3"
  end

  config.vm.define "targetvm", autostart: true do |targetvm|
    targetvm.vm.synced_folder "target_share", "/home/vagrant/share", disabled: false, create: true
    targetvm.vm.hostname = "targetvm"
    targetvm.vm.network :private_network, ip: "172.28.128.4"
  end

  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "512"
  end

end
