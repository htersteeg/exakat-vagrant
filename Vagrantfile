# -â€‹*- mode: ruby -*â€‹-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

 config.vm.define "default"

 # Enable Hostmanger (Puts hostname in local hosts file
 config.hostmanager.enabled = true
 config.hostmanager.manage_host = true
 config.hostmanager.ignore_private_ip = false
 config.hostmanager.include_offline = true
 config.vm.box = "boxcutter/ubuntu1604"
#config.vm.box = "parallels/debian-8.2"
   
 config.vm.hostname = "vagrant-exakat.dev"
 config.vm.network "private_network", ip: "192.168.55.55"
 config.vm.synced_folder "./", "/home/vagrant/sync", owner: "vagrant", group: "vagrant"
 config.vm.provider :virtualbox do |vb|
   vb.gui = false
   vb.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]
    vb.customize [
                "modifyvm", :id,
                "--cableconnected1", "on",
            ]
 end

 config.vm.network "forwarded_port", guest: 7474, host: 7474

 config.vm.provision "ansible_local" do |ansible|
   ansible.verbose = "vvvv"
   ansible.version = "latest"
   ansible.raw_arguments = ['--timeout=300']
   ansible.sudo = true
   ansible.playbook = ".ansible/exakat.yml"
 end
end
