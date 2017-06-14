# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", 256]
  end

  config.vm.define :balancer1, primary: true do |balancer1_config|
    balancer1_config.vm.hostname = 'balancer1'  
    balancer1_config.vm.network :private_network, ip: "192.168.1.50"
    balancer1_config.vm.provision "shell" do |s|
      s.path = "balancer-setup.sh"
      s.args = "101"
    end
  end

  config.vm.define :balancer2, primary: true do |balancer2_config|
    balancer2_config.vm.hostname = 'balancer2'
    balancer2_config.vm.network :private_network, ip: "192.168.1.51"
    balancer2_config.vm.provision "shell" do |s|
      s.path = "balancer-setup.sh"
      s.args = "100"
    end
  end

  config.vm.define :app1 do |app1_config|
    app1_config.vm.hostname = 'app1'
    app1_config.vm.network :private_network, ip: "192.168.1.52"
    app1_config.vm.provision :shell, :path => "app-setup.sh"
  end

  config.vm.define :app2 do |app2_config|
    app2_config.vm.hostname = 'app2'
    app2_config.vm.network :private_network, ip: "192.168.1.53"
    app2_config.vm.provision :shell, :path => "app-setup.sh"
  end
end
