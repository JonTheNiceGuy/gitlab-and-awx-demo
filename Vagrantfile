# This Vagrantfile tells Vagrant how to stand up a Virtualbox machine running Ubuntu Server.
# It then tells the server to install Ansible, and then use Ansible to make system changes.
#
# You must have at least:
# * Vagrant from https://vagrantup.com
# * Virtualbox from https://virtualbox.org
# * The *SAME VERSION* extensions from Virtualbox as the version you've downloaded
#
# Install Virtualbox, then install the Extension to Virtualbox, then finally Vagrant.
# It doesn't really matter if you do Vagrant and Virtualbox the other way around, but
# you *need* the extension pack for Virtualbox, otherwise the disks won't mount.

# While it is not a requirement, I would suggest you install the following plugin for Vagrant:
# vagrant plugin install vagrant-vbguest

Vagrant.configure("2") do |config|
  config.vm.define "awx" do |awx|
    awx.vm.box = "ubuntu/bionic64"
    awx.vm.hostname = "awx"
    awx.vm.box_check_update = false
    awx.vm.boot_timeout = 0
    if Vagrant.has_plugin?("vagrant-cachier")
      awx.cache.scope = :box
    end
    awx.vm.box_check_update = false
    awx.vm.network "public_network", bridge: "enp0s25", ip: "192.168.1.35", :use_dhcp_assigned_default_route => true
    # awx.vm.network "private_network", ip: "192.0.2.100"
    # awx.vm.synced_folder "../data", "/vagrant_data"
    awx.vm.provider "virtualbox" do |vb|
      vb.memory = 8196
      vb.cpus = 3
      vb.name = "AWX"
    end
    awx.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "install_awx.yml"
      ansible.install_mode   = "pip"
    end
  end
end
