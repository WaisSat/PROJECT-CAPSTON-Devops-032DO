Vagrant.configure("2") do |config|
  config.vm.box = "bandit145/centos_stream9_arm"
  
  # Provisioning: Ensure sudo works for Ansible without password prompts
  config.vm.provision "shell", inline: <<-SHELL
    echo "vagrant ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/vagrant
    chmod 0440 /etc/sudoers.d/vagrant
  SHELL

  config.vm.provider "vmware_desktop" do |v|
    v.gui = false 
    v.allowlist_verified = true
  end

  # --- REQUIRED SERVERS ---

  # DNS
  config.vm.define "prdx-dns101" do |node|
    node.vm.hostname = "prdx-dns101"
    node.vm.network "private_network", ip: "192.168.56.10"
    node.vm.provider "vmware_desktop" do |v| v.memory = 1024; v.cpus = 1; end
  end

  # Database
  config.vm.define "prdx-db101" do |node|
    node.vm.hostname = "prdx-db101"
    node.vm.network "private_network", ip: "192.168.56.11"
    node.vm.provider "vmware_desktop" do |v| v.memory = 1024; v.cpus = 1; end
  end

  # Web Servers
  ["101", "102", "103"].each do |i|
    config.vm.define "prdx-webserver#{i}" do |node|
      node.vm.hostname = "prdx-webserver#{i}"
      node.vm.network "private_network", ip: "192.168.56.2#{i.to_i - 100}"
      node.vm.provider "vmware_desktop" do |v| v.memory = 1024; v.cpus = 1; end
    end
  end

  # Load Balancer
  config.vm.define "prdx-haproxy101" do |node|
    node.vm.hostname = "prdx-haproxy101"
    node.vm.network "private_network", ip: "192.168.56.30"
    node.vm.provider "vmware_desktop" do |v| v.memory = 1024; v.cpus = 1; end
  end

  # Nagios
  config.vm.define "prdx-nagios101" do |node|
    node.vm.hostname = "prdx-nagios101"
    node.vm.network "private_network", ip: "192.168.56.40"
    node.vm.provider "vmware_desktop" do |v| v.memory = 1024; v.cpus = 1; end
  end

  # Ansible
  config.vm.define "prdx-ansible101" do |node|
    node.vm.hostname = "prdx-ansible101"
    node.vm.network "private_network", ip: "192.168.56.50"
    node.vm.provider "vmware_desktop" do |v| v.memory = 1024; v.cpus = 1; end
  end

  # Docker Primary
  config.vm.define "prdx-dprimary101" do |node|
    node.vm.hostname = "prdx-dprimary101"
    node.vm.network "private_network", ip: "192.168.56.60"
    node.vm.provider "vmware_desktop" do |v| v.memory = 4096; v.cpus = 4; end
  end

  # Kubernetes 
  config.vm.define "prdx-kube101" do |node|
    node.vm.hostname = "prdx-kube101"
    node.vm.network "private_network", ip: "192.168.56.70"
    node.vm.network "forwarded_port", guest: 8443, host: 8443
    node.vm.network "forwarded_port", guest: 9090, host: 9090  
    node.vm.provider "vmware_desktop" do |v| 
      v.memory = 3072
      v.cpus = 1
    end
  end

end

