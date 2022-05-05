# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "load-balancer" do |vm1|
    vm1.vm.hostname = "load-balancer"
    vm1.vm.box = "ubuntu/bionic64"
    vm1.vm.network "private_network", ip: "192.168.55.10"
    vm1.vm.synced_folder "./resources/", "/home/vagrant/resources/", create: true

    vm1.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("/tmp/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
    echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
    echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
    end

    vm1.vm.provider "virtualbox" do |vb|
      vb.name = "load-balancer"
      vb.gui = false
      vb.memory = "1024"
    end

  end


  config.vm.define "web-1" do |vm2|
    vm2.vm.hostname = "web-1"
    vm2.vm.box = "ubuntu/bionic64"
    vm2.vm.network "private_network", ip: "192.168.55.20"
    vm2.vm.synced_folder "./resources/", "/home/vagrant/resources/", create: true
    
    vm2.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("/tmp/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
    echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
    echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
    end

    vm2.vm.provider "virtualbox" do |vb|
      vb.name = "web-1"
      vb.gui = false
      vb.memory = "1024"
    end
  end


  config.vm.define "web-2" do |vm3|
    vm3.vm.hostname = "web-2"
    vm3.vm.box = "ubuntu/bionic64"
    vm3.vm.network "private_network", ip: "192.168.55.30"
    vm3.vm.synced_folder "./resources/", "/home/vagrant/resources/", create: true

    vm3.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("/tmp/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
    echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
    echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
    SHELL
    end

    vm3.vm.provider "virtualbox" do |vb|
      vb.name = "web-2"
      vb.gui = false
      vb.memory = "1024"
    end
  end
  
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "./ansible/install-docker.yml"
  end

end


#~/.ssh/authorized_keys - public key
#~/.ssh/ - private key


# config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/id_rsa.pub"
