# Vagrant + Concrete5

## Getting Started

1. Install VirtualBox.
 * https://www.virtualbox.org/
2. Install Vagrant.
 * http://www.vagrantup.com/
3. Install the vagrant plugins.
 * `vagrant plugin install vagrant-omnibus`
 * `vagrant plugin install vagrant-berkshelf`
4. Clone the repository into a local directory.
 * `git clone https://github.com/miya0001/vagrant-concrete5.git`
5. Change into a new directory.
 * `cd vagrant-concrete5`
6. Install cookbooks.
 * `berks install -p cookbooks`
7. Start a Vagrant environment.
 * `vagrant up`
8. Visit http://127.0.0.1:8080/

## Configuration

See attributes.
https://github.com/Launch-with-1-Click/concrete5

## Contributors

* [@miya0001](https://github.com/miya0001/)
