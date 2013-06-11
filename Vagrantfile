# -*- mode: ruby -*-
# vi: set ft=ruby :
#^syntax detection

Vagrant::Config.run do |config|
  config.vm.box = 'precise32'
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  config.vm.forward_port 80, 8000
  config.vm.forward_port 8080, 8001
  config.vm.forward_port 8125, 8125, :protocol => 'udp'

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe 'apt'
    chef.add_recipe 'graphite'
    chef.add_recipe 'nodejs'
    chef.add_recipe 'statsd'
  end

end
