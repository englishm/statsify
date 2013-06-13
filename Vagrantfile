# -*- mode: ruby -*-
# vi: set ft=ruby :
#^syntax detection
Vagrant.configure('2') do |config|

  config.vm.provider :digital_ocean do |provider|
    provider.box = 'do_statsify'
    provider.client_id = ENV['DO_CLIENT_ID']
    provider.api_key = ENV['DO_API_KEY']
    provider.region = 'Amsterdam 1'
    provider.image = 'Ubuntu 12.04 x32 Server'
  end

  config.vm.define :local do |local_config|
    local_config.vm.box = 'precise32'
    local_config.vm.box_url = "http://files.vagrantup.com/precise32.box"
    local_config.vm.network :forwarded_port, guest: 8080, host: 8001
    local_config.vm.network :forwarded_port, guest: 80, host: 8000
    local_config.vm.network :forwarded_port, guest: 8125, host: 8125, :protocol => 'udp'
    shared_config! local_config
  end

  config.vm.define :cloud do |cloud_config|
    cloud_config.vm.host_name = 'statsify'
    cloud_config.vm.box = 'digital_ocean'
    cloud_config.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"
    cloud_config.ssh.private_key_path = ENV['SSH_KEY_PATH']
    shared_config! cloud_config
  end

end

def shared_config!(config)
    config.vm.synced_folder '.', '/vagrant'
    config.omnibus.chef_version = :latest
    config.vm.provision :chef_solo do |chef|
      chef.add_recipe 'apt'
      chef.add_recipe 'vim'
      chef.add_recipe 'graphite'
      chef.add_recipe 'nodejs'
      chef.add_recipe 'statsd'

      chef.json = {
        :nodejs => {
          :version => '0.10.10',
          :npm => '1.2.25'
        }
      }
    end
end
