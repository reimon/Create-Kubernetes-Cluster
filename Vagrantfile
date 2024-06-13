Vagrant.configure("2") do |config|
    config.vm.box = "sloopstash/ubuntu-22-04"
    config.vm.box_version = "2.1.1"
    config.vm.define "ubuntu-22-04-server"
    config.vm.hostname = "k8s-CP"
    config.vm.box_check_update = false
    config.vm.disk :disk, size:"30GB", primary: true  
    config.vm.network "forwarded_port", guest: 81, host: 81
    config.vm.network "forwarded_port", guest: 80, host: 80
    config.vm.network "forwarded_port", guest: 3306, host: 3306
    config.vm.network "forwarded_port", guest: 8080, host: 8080
    config.vm.network "forwarded_port", guest: 9000, host: 9000
    config.vm.network "forwarded_port", guest: 19999, host: 19999
    config.vm.network "forwarded_port", guest: 9001, host:9001

    config.vm.network "public_network", ip: "192.168.0.47"
    
    # Disabling share 
   
    #config.vm.synced_folder "./config", "/config", create: true, disabled: true
    config.vm.synced_folder ".", "/vagrant", disabled: true
  
    # SSH credentials to connect to virtual machine.
    config.ssh.username = "vagrant"
    config.ssh.private_key_path = ["~/.vagrant.d/insecure_private_key"]
    config.ssh.insert_key = false

    config.vm.provider "vmware_fusion" do |vb|
      # Disable GUI when booting the virtual machine.
      vb.gui = false
    
      # Allocate memory to the virtual machine.
      vb.memory = "15048"
      # Allocate processors to the virtual machine.
      vb.cpus = "4"
  
    end

  end
  
