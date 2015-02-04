# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "mac-osx-10-10"
  config.vm.box_url = "./mac-osx-10-10.box"

  config.ssh.insert_key = false

  # Prevent asking for password when no GUI is available
  config.vm.provision "shell", path: "./setup-keychain.sh", privileged: false

  config.vm.define "base" do |base|
  end

  config.vm.define "boxen" do |boxen|
    boxen.vm.synced_folder "our-boxen", "/opt/boxen/repo", type: "nfs"

    $boxen_provisioning = "cd /opt/boxen/repo; " <<
      "./script/boxen --no-fde --debug --token=" << (ENV['GH_TOKEN'] || "")
    boxen.vm.provision "shell", inline: $boxen_provisioning, privileged: false
  end
end
