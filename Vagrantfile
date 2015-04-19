# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define 'wordpress-php55', autostart: false do |node|
    node.vm.box = 'base'
    node.vm.hostname = 'wordpress.local'
    node.vm.network :private_network, ip: '192.168.33.10'

    node.vm.provider :virtualbox do |vb|
      vb.customize [
        'modifyvm', :id,
        '--memory', '512',
      ]
    end

    node.vm.provision :shell, :path => "puppet/bootstrap.sh"
    node.vm.provision :puppet do |puppet|
      puppet.facter = { 'fqdn' => node.vm.hostname }
      puppet.manifests_path = "puppet/manifests"
      puppet.manifest_file  = "wordpress-php55.pp"
    end
  end

end
