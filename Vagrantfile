# -*- mode: ruby -*-
# vi: set ft=ruby :
#^syntax detection

Vagrant.configure('2') do |config|
  config.vm.box = 'precise32'
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  # config.vm.forward_port 80, 8000
  # config.vm.forward_port 8080, 8001
  # config.vm.forward_port 8125, 8125, :protocol => 'udp'

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe 'apt'
    chef.add_recipe 'graphite'
    chef.add_recipe 'nodejs'
    chef.add_recipe 'statsd'
  end

  config.vm.synced_folder '.', '/vagrant'
  config.omnibus.chef_version = :latest

  config.vm.provider :digital_ocean do |provider|
    provider.client_id = ENV['DO_CLIENT_ID']
    provider.api_key = ENV['DO_API_KEY']
    provider.region = 'Amsterdam 1'
    provider.image = 'Ubuntu 12.04 x32 Server'
    
    config.ssh.private_key_path = '~/.ssh/digital-ocean'
  end
end
