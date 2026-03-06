Vagrant.configure("2") do |config|
  # Define servers based on Project: Devops 032DO specifications
  # Note: Rocky 9 used for modern servers, Ubuntu/Generic for older requirement compatibility
  servers = [
    { name: "dns101",        box: "gyptazy/rocky9.3-arm64", mem: 1024, ip: "192.168.56.10" },
    { name: "db101",         box: "gyptazy/rocky9.3-arm64", mem: 1024, ip: "192.168.56.12" },
    { name: "webserver101",  box: "ubuntu/arm64/22.04",     mem: 1024, ip: "192.168.56.13" },
    { name: "webserver102",  box: "ubuntu/arm64/22.04",     mem: 1024, ip: "192.168.56.14" },
    { name: "webserver103",  box: "ubuntu/arm64/22.04",     mem: 1024, ip: "192.168.56.15" },
    { name: "haproxy101",    box: "ubuntu/arm64/22.04",     mem: 1024, ip: "192.168.56.16" },
    { name: "nagios101",     box: "ubuntu/arm64/22.04",     mem: 1024, ip: "192.168.56.17" },
    { name: "ansible101",    box: "gyptazy/rocky9.3-arm64", mem: 1024, ip: "192.168.56.11" },
    { name: "dprimary101",   box: "gyptazy/rocky9.3-arm64", mem: 4096, ip: "192.168.56.18" },
    { name: "kube101",       box: "gyptazy/rocky9.3-arm64", mem: 3072, ip: "192.168.56.19" }
  ]

  servers.each do |server|
    config.vm.define server[:name] do |node|
      node.vm.box = server[:box]
      node.vm.hostname = server[:name]
      node.vm.network "private_network", ip: server[:ip]

      node.vm.provider "vmware_desktop" do |v|
        v.gui = false
        v.memory = server[:mem]
      end

      # Provisioning: Ensure 'ansible' user exists with password 'password'
      # and sudo privileges per project requirements
      node.vm.provision "shell", inline: <<-SHELL
        useradd -m -s /bin/bash ansible || true
        echo "ansible:password" | chpasswd
        echo "ansible ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ansible
        chmod 0440 /etc/sudoers.d/ansible
      SHELL
    end
  end
end
