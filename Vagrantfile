Vagrant.configure("2") do |config|

  config.vm.provider :libvirt do |libvirt|
       libvirt.host = "localhost"
       libvirt.uri = "qemu:///system"
       libvirt.management_network_name = "default"
       libvirt.management_network_address = "192.168.122.0/24"
  end

  config.vm.define :node do |node|
    config.ssh.insert_key = false
    config.ssh.private_key_path = ["~/.ssh/vagrant/vagrant_rsa_key"]
    node.vm.hostname = "vm-debian10"
    node.vm.synced_folder "./shared", "/opt/vagrant/data"
    node.vm.box = "debian10"
    node.vm.network "private_network", ip: "192.168.122.253"
    node.vm.provider :libvirt do |domain|
      domain.memory = 2048
      domain.cpus = 2
    end
    node.vm.provision "shell", path: "./shared/bootstrap.sh"
  end

end
