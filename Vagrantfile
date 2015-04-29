require_relative './vagrant/key_authorization'

# We need this plugin for resolving host names
unless Vagrant.has_plugin?("vagrant-hostsupdater")
  raise 'vagrant-hostsupdater plugin is not installed! Please install...'
end

Vagrant.configure('2') do |config|
  config.vm.box = 'chef/debian-7.4'
  authorize_key_for_root config, '~/.ssh/id_dsa.pub', '~/.ssh/id_rsa.pub'

  {
      'mesos-master'    => '192.168.33.11',
      'mesos-master2'   => '192.168.33.14',
      'mesos-master3'   => '192.168.33.15',
      'mesos-slave1'    => '192.168.33.12',
      'mesos-slave2'    => '192.168.33.13',
  }.each do |short_name, ip|
    config.vm.define short_name do |host|
      host.vm.network 'private_network', ip: ip
      host.vm.hostname = "#{short_name}"
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.host_key_checking = false
      ansible.inventory_path = "inventory"
      ansible.extra_vars = { ansible_ssh_user: 'root', ansible_ssh_private_key_file: '~/.ssh/id_rsa'}
      end
    end
  end
end
