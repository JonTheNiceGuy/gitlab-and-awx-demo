# This Vagrantfile tells Vagrant how to stand up a Virtualbox machine running Ubuntu Server.
# It then tells the server to install Ansible, and then use Ansible to make system changes.
#
# You must have at least:
# * Vagrant from https://vagrantup.com
# * Virtualbox from https://virtualbox.org

# While it is not a requirement, I would suggest you install the following plugin for Vagrant,
# particularly if you plan on building this from a destroyed version at all often:
# vagrant plugin install vagrant-cachier

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
#   Pick one - Public Network (with ports 80 - AWX and 1080 - Gitlab)
#    awx.vm.network "public_network", :use_dhcp_assigned_default_route => true
#   Or forwarded ports, as listed below...
    awx.vm.network "forwarded_port", guest:   80, host: 10080, protocol: "tcp" # AWX HTTP
    awx.vm.network "forwarded_port", guest: 1080, host: 11080, protocol: "tcp" # Gitlab HTTP
    awx.vm.network "forwarded_port", guest: 2222, host: 12222, protocol: "tcp" # Gitlab SSH
    awx.vm.provider "virtualbox" do |vb|
#     This is probably insufficient memory, but it just about works. Sometimes gitlab dies.
      vb.memory = 5120
      vb.cpus = 4
      vb.name = "awx"
    end
    awx.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "install_awx.yml"
      ansible.install_mode   = "pip"
    end
  end
end
