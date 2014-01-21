# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :forwarded_port, guest: 80, host: 8080

  config.omnibus.chef_version = :latest
  config.berkshelf.enabled = true

  File.open('Berksfile', 'w').write <<-EOS
    cookbook 'concrete5', git: "https://github.com/Launch-with-1-Click/concrete5.git"
  EOS

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe "concrete5"
    chef.json = {
        :mysql => {
            :server_debian_password => "concrete5",
            :server_root_password   => "concrete5",
            :server_repl_password   => "concrete5"
        },
        :concrete5 => {
            :site => 'Welcome to the Concrete5'
        }
    }
  end

end
