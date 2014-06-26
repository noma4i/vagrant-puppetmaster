# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define :master do |master_config|
    # Supports local cache, don't wast bandwitdh
    # vagrant plugin install vagrant-cachier
    # https://github.com/fgrehm/vagrant-cachier 
    if Vagrant.has_plugin?("vagrant-cachier")
      config.cache.auto_detect = true
    end
      master_config.vm.hostname = "puppet"
      master_config.vm.box = "precise64"
      master_config.vm.box_url = "http://files.vagrantup.com/precise64.box"
      master_config.vm.network :private_network, ip: "192.168.33.10"
      master_config.vm.provider :virtualbox do |vb|
        vb.customize [
          'modifyvm', :id,
          '--name', 'puppetmaster',
          '--memory', '512'
        ]
      end
        
      # Share an additional folder to the guest VM. The first argument is
      # an identifier, the second is the path on the guest to mount the
      # folder, and the third is the path on the host to the actual folder.
      
      master_config.vm.provision :shell, :path => "puppet_master.sh"

    master_config.vm.synced_folder "puppet", "/etc/puppet"
  end
  
  
end
