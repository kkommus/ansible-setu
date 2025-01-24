Vagrant.configure("2") do |config|

  # Dockerhost - Debian 12
  config.vm.define "keitikommus-dockerhost" do |dockerhost|
    dockerhost.vm.box = "generic/debian12"
    dockerhost.vm.box_version = "4.3.12"
    dockerhost.vm.network "private_network", ip: "10.10.10.130", virtualbox__intnet: "ansible_keitikommus"
    dockerhost.vm.hostname = "keitikommus-dockerhost"
    dockerhost.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "8192"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.name = "KEITIKOMMUS-DOCKERHOST"
    end

    dockerhost.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io snmpd tmux mc wget tree git
    SHELL
  end

  # Ansible - Debian 12
  config.vm.define "keitikommus-ansible" do |ansible|
    ansible.vm.box = "generic/debian12"
    ansible.vm.box_version = "4.3.12"
    ansible.vm.network "private_network", ip: "10.10.10.131", virtualbox__intnet: "ansible_keitikommus"
    ansible.vm.hostname = "keitikommus-ansible"
    ansible.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
      vb.name = "KEITIKOMMUS-ANSIBLE"
    end

    # Sünkroonimiskaust
    ansible.vm.synced_folder "C:/ANSIBLE/ansible_data", "/vagrant_data"

    ansible.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y ansible sshpass yamllint ansible-lint snmpd tmux mc wget tree git
    SHELL
  end

  # Ubuntu 24.04
  config.vm.define "keitikommus-ubuntu" do |ubuntu|
    ubuntu.vm.box = "bento/ubuntu-24.04"
    ubuntu.vm.box_version = "202404.26.0"
    ubuntu.vm.network "private_network", ip: "10.10.10.132", virtualbox__intnet: "ansible_keitikommus"
    ubuntu.vm.hostname = "keitikommus-ubuntu"
    ubuntu.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
      vb.name = "KEITIKOMMUS-UBUNTU"
    end

    ubuntu.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y snmpd tmux mc wget tree git
    SHELL
  end

  # CentOS Stream 9
  config.vm.define "keitikommus-centos" do |centos|
    centos.vm.box = "centos/stream9"
    centos.vm.box_version = "20250122.0"
    centos.vm.network "private_network", ip: "10.10.10.133", virtualbox__intnet: "ansible_keitikommus"
    centos.vm.hostname = "keitikommus-centos"
    centos.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
      vb.name = "KEITIKOMMUS-CENTOS"
    end

    centos.vm.provision "shell", inline: <<-SHELL
      yum update -y
      yum install -y epel-release
      yum install -y snmpd tmux mc wget tree git
    SHELL
  end

  # OpenSUSE Leap
  config.vm.define "keitikommus-opensuse" do |opensuse|
    opensuse.vm.box = "bento/opensuse-leap-15"
    opensuse.vm.network "private_network", ip: "10.10.10.134", virtualbox__intnet: "ansible_keitikommus"
    opensuse.vm.hostname = "keitikommus-opensuse"
    opensuse.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "2048"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
      vb.name = "KEITIKOMMUS-OPENSUSE"
    end

    opensuse.vm.provision "shell", inline: <<-SHELL
      sudo zypper refresh
      sudo zypper install -y net-snmp tmux mc wget tree git
    SHELL
  end

end
