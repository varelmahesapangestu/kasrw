Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"

  config.vm.define "vm-database" do |db|
    db.vm.box = "bento/ubuntu-22.04"
    db.vm.hostname = "vm-database"
    db.vm.network "private_network", ip: "192.168.56.11"

    db.vm.provider "virtualbox" do |vb|
      vb.name = "vm-database"
      vb.memory = "1024"
      vb.cpus = 1
    end
  end

  config.vm.define "vm-backend" do |backend|
    backend.vm.box = "bento/ubuntu-22.04"
    backend.vm.hostname = "vm-backend"
    backend.vm.network "private_network", ip: "192.168.56.10"

    backend.vm.provider "virtualbox" do |vb|
      vb.name = "vm-backend"
      vb.memory = "1024"
      vb.cpus = 1
    end

    backend.vm.provision "shell", inline: <<-SHELL
      cp /vagrant/ansible/insecure_private_key /home/vagrant/insecure_private_key
      chmod 600 /home/vagrant/insecure_private_key
      chown vagrant:vagrant /home/vagrant/insecure_private_key
    SHELL

    backend.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "ansible/inventory"
      ansible.limit = "all"
    end
  end


  config.vm.define "vm-frontend" do |fe|
    fe.vm.box = "bento/ubuntu-22.04"
    fe.vm.hostname = "vm-frontend"
    fe.vm.network "private_network", ip: "192.168.56.12"

    fe.vm.provider "virtualbox" do |vb|
      vb.name = "vm-frontend"
      vb.memory = "1024"
      vb.cpus = 1
    end
  end

end