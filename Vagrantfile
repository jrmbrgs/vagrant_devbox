require 'vagrant-omnibus'

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "precise32"
    config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    config.vm.network "forwarded_port", guest: 80, host: 8088
    config.vm.synced_folder "w", "/w"

    # use omnibus to keep chef at the latest version on vm
    config.omnibus.chef_version = :latest

    config.vm.provision :chef_solo do |chef|
        chef.cookbooks_path = "chef/cookbooks"
        chef.custom_config_path = "chef.conf"

        chef.json = { 
            :apache => {
                :default_site_enabled => true, # just for testing
                :listen_ports => [ "80" ]
            }
        }
        
        chef.add_recipe "apt"
        chef.add_recipe "build-essential"
        chef.add_recipe "vim"
        chef.add_recipe "git"
        chef.add_recipe "chef-dotdeb::php54"
        chef.add_recipe "php"
        chef.add_recipe "apache2"
        chef.add_recipe "apache2::mod_rewrite"
        chef.add_recipe "apache2::mod_php5"
        chef.add_recipe "mysql::server"
        chef.add_recipe "mysql::client"
       #chef.add_recipe "nginx"
       #chef.add_recipe "nodejs"
    end
end
