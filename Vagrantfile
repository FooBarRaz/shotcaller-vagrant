# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

#Replace this with the path to your shotcaller git directory
SHOTCALLER_SRC_PATH="C:\\Users\\Raz\\dev\\shotcaller"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.omnibus.chef_version = "12.21.26"

	config.vm.synced_folder SHOTCALLER_SRC_PATH, "/home/ubuntu/shotcaller"

	config.vm.box = "ubuntu/xenial64"

	# Configure the virtual machine to use 1.5GB of RAM
	config.vm.provider :virtualbox do |vb|
		vb.customize ["modifyvm", :id, "--memory", "4096"]
	end

	# Forward the Rails server default port to the host
	config.vm.network :forwarded_port, guest: 3000, host: 3000

	# Use Chef Solo to provision our virtual machine
	config.vm.provision :chef_solo do |chef|
		chef.cookbooks_path = ["cookbooks", "site-cookbooks"]

		chef.add_recipe "apt"
		chef.add_recipe "build-essential"
		chef.add_recipe "system::install_packages"
		chef.add_recipe "ruby_build"
		chef.add_recipe "ruby_rbenv::user"
		chef.add_recipe "ruby_rbenv::user_install"
		chef.add_recipe "vim"
		chef.add_recipe "postgresql::server"
		chef.add_recipe "postgresql::client"
    chef.add_recipe "heroku"

		chef.json = {
			rbenv: {
				user_installs: [{
					user: 'ubuntu',
					rubies: ["2.2.4"],
					global: "2.2.4",
					gems: {
						"2.2.4" => [{ name: "bundler" }]
					}
				}]
		  },

			system: {
				packages: {
					install: ["redis-server", "nodejs", "libpq-dev", "tree"]
				}
			},

			postgresql: {
				:pg_hba => [{
					:comment => "# Add vagrant role",
					:type => 'local', :db => 'all', :user => 'ubuntu', :addr => nil, :method => 'trust'
				}],
				:users => [{
					"username": "ubuntu",
					"password": "",
					"superuser": true,
					"replication": false,
					"createdb": true,
					"createrole": false,
					"inherit": false,
					"login": true
				}]
			}
    }
		end
end
