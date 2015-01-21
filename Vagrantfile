# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

#
# Configuration
#

VM_BOX              = "hashicorp/precise64" # Ubuntu 12.04
# VM_BOX              = "chef/centos-6.5" # CentOS 6.5

C5_HOSTNAME         = "concrete5.local" # e.g example.com
C5_IP               = "192.168.33.35" # host ip address
C5_LOCALE           = "ja_JP"

C5_GIT_REPOSITORY   = "https://github.com/concrete5/concrete5-5.7.0.git"
C5_GIT_REVISION     = "5.7.3"
# C5_GIT_REPOSITORY   = "https://github.com/concrete5/concrete5.git"
# C5_GIT_REVISION     = "5.6.3.2"


C5_TITLE            = "Welcome to the concrete5" # site title

C5_ADMIN_EMAIL      = "admin@example.com" # concrete5 admin email
C5_ADMIN_PASSWORD   = "concrete5" # concrete5 admin password

C5_DB_NAME          = "concrete5"
C5_DB_PASS          = "concrete5"
C5_DB_USER          = "concrete5"

C5_STARTING_POINT   = "elemental_blank" # elemental_blank or elemental_full.
# C5_STARTING_POINT   = "blank" # for 5.6

# End configuration


if VM_BOX === "hashicorp/precise64"
    PHP_PACKAGES = %w{ php5-cgi php5 php5-dev php5-cli php-pear }
elsif VM_BOX === "chef/centos-6.5"
    PHP_PACKAGES = %w{ php php-devel php-cli php-pear php-mbstring }
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = VM_BOX

  config.vm.hostname = C5_HOSTNAME
  config.vm.network :private_network, ip: C5_IP

  config.vm.synced_folder "www/concrete5", "/var/www/concrete5", :create => true

  if Vagrant.has_plugin?("vagrant-hostsupdater")
    config.hostsupdater.remove_on_suspend = true
  end

  config.omnibus.chef_version = :latest

  config.vm.provision :chef_solo do |chef|
    chef.add_recipe "concrete5"
    chef.json = {
        :apache => {
            :user   => 'vagrant',
            :group  => 'vagrant'
        },
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
            :packages => PHP_PACKAGES
        },
        # See https://github.com/torounit/concrete5
        :concrete5 => {
            :db => {
              :name => C5_DB_NAME,
              :pass => C5_DB_PASS,
              :user => C5_DB_USER
            },
            :locale         => C5_LOCALE,
            :starting_point => C5_STARTING_POINT,
            :git_repository => C5_GIT_REPOSITORY,
            :git_revision   => C5_GIT_REVISION,
            :site           => C5_TITLE,
            :admin => {
                :email      => C5_ADMIN_EMAIL,
                :password   => C5_ADMIN_PASSWORD
            }
        }
    }
  end

end
