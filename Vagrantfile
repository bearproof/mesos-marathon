require_relative './vagrant/key_authorization'

# We need this plugin for resolving host names
unless Vagrant.has_plugin?("vagrant-hostsupdater")
  raise 'vagrant-hostsupdater plugin is not installed! Please install...'
end

Vagrant.configure('2') do |config|
  config.vm.box = 'chef/centos-7.0'
  authorize_key_for_root config, '~/.ssh/id_dsa.pub', '~/.ssh/id_rsa.pub'

  {
      'mesos-master'    => '192.168.33.11',
      'mesos-slave1'    => '192.168.33.12',
      'mesos-slave2'    => '192.168.33.13',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}"
    end
  end
end