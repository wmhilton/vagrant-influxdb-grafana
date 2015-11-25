# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
puts "DIGITALOCEAN_TOKEN = #{ENV['DIGITALOCEAN_TOKEN']}"
# Tip: Run 'vagrant plugin install vagrant-vbguest'

## Random password generator (work in progress)
#require 'securerandom'
#bob = SecureRandom.base64
#puts bob

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "influxdb-grafana-ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/trusty64"
    ubuntu.vm.network :private_network, ip: "192.168.33.21"

    ubuntu.vm.network "forwarded_port", :guest => 8083, :host => 8083
    ubuntu.vm.network "forwarded_port", :guest => 8086, :host => 8086
    ubuntu.vm.network "forwarded_port", :guest => 3000, :host => 3000

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

  # Tip: Run 'vagrant plugin install vagrant-digitalocean'
  #      And 'vagrant box add digital_ocean https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box'
  config.vm.provider "digital_ocean" do |provider, override|
    # Tip: Run 'ssh-keygen -f ~/.ssh/Vagrant'
    override.ssh.private_key_path = "~/.ssh/Vagrant"
    override.vm.box = "digital_ocean"
    override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.token = ENV['DIGITALOCEAN_TOKEN']
    provider.image = "ubuntu-14-04-x64"
    provider.region = "nyc3"
    provider.size = '1gb'
    provider.name = 'influxdb'
    provider.private_networking = true

    provider.vm.provision "shell" do |s|
      s.inline = "sudo apt-get install ansible -y"
    end
    provider.vm.provision "shell" do |s|
      s.inline = "ansible-playbook -i \"localhost,\" -c local /vagrant/dashboard.yml"
    end
  end

end
