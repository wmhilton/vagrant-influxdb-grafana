# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "influxdb-grafana-ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/trusty64"
    ubuntu.vm.network :private_network, ip: "192.168.33.21"

    ubuntu.vm.network "forwarded_port", :guest => 8083, :host => 8083
    ubuntu.vm.network "forwarded_port", :guest => 8086, :host => 8086
    ubuntu.vm.network "forwarded_port", :guest => 8090, :host => 8090
    ubuntu.vm.network "forwarded_port", :guest => 8099, :host => 8099

    ubuntu.vm.provision "shell" do |s|
      s.inline = "sudo apt-get install ansible -y"
    end
    ubuntu.vm.provision "shell" do |s|
      s.inline = "ansible-playbook -i \"localhost,\" -c local /vagrant/dashboard.yml"
    end
  end

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "1024"]
  end

end
