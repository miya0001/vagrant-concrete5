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
        :php => {
            :directives => {
                :default_charset             => 'UTF-8',
                'mbstring.language'          => 'neutral',
                'mbstring.internal_encoding' => 'UTF-8',
                'date.timezone'              => 'UTC'
            },
            :packages => %w{ php5-cgi php5 php5-dev php5-cli php-pear } # ubuntu
            # :packages => %w{ php php-devel php-cli php-pear php-mbstring } #centos
        },
        # See https://github.com/Launch-with-1-Click/concrete5
        :concrete5 => {
            :git_repository => 'https://github.com/concrete5/concrete5.git',
            :git_revision   => '5.6.2.1',
            :cli_url        => 'https://raw2.github.com/concrete5/concrete5/master/cli/install-concrete5.php',
            :site           => 'Welcome to the Concrete5',
            :admin => {
                :email      => 'admin@example.com',
                :password   => 'concrete5'
            }
        }
    }
  end

end
