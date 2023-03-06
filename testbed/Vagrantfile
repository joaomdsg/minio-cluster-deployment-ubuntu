Vagrant.configure("2") do |config|
    # Set VirtualBox as the virtualization layer
    config.vm.provider "virtualbox"

    # Set the base box to use
    config.vm.box = "ubuntu/jammy64"

    # Define the two virtual machines
    config.vm.define "minio1" do |node|
      node.vm.hostname = "minio1"

      # Set an interface with a static IP address
      node.vm.network "private_network", ip: "192.168.50.101"

      
      node.vm.provider "virtualbox" do |v|
        # Set CPU and RAM
        v.memory = "2048"
        v.cpus = "2"
        # Create two 1GB drives
        v.customize ['createhd', '--filename', 'minio1_drive1.vdi', '--size', '1000']
        v.customize ['createhd', '--filename', 'minio1_drive2.vdi', '--size', '1000']
        # Attach the drives
        v.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', 'minio1_drive1.vdi']
        v.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', 'minio1_drive2.vdi']
    
      end
    end
  
    config.vm.define "minio2" do |node|
      node.vm.hostname = "minio2"

      # Set an interface with a static IP address
      node.vm.network "private_network", ip: "192.168.50.102"
      
      node.vm.provider "virtualbox" do |v|
        v.memory = "2048"
        v.cpus = "2"
        # Create two  1GB drives
        v.customize ['createhd', '--filename', 'minio2_drive1.vdi', '--size', '1000']
        v.customize ['createhd', '--filename', 'minio2_drive2.vdi', '--size', '1000']
        # Attach the drives
        v.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', 'minio2_drive1.vdi']
        v.customize ['storageattach', :id, '--storagectl', 'SCSI', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', 'minio2_drive2.vdi']

      end
    end
  end

