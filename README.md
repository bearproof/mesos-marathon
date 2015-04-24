# Mesos Marathon Cluster
A complete cluster running Apache Mesos, Marathon, Mesos DNS, Chronos, Docker and Ansible.


## Preconditions

### Vagrant
- **vagrant-hostsupdater** plugin, to be able to map names to ip addresses. For more info about this plugin, take a look [here](https://github.com/cogitatio/vagrant-hostsupdater).

## SSH access to VMs

This two sections of the Vagrantfile add your public key to the list of root authorized_keys on the VMs. After you do a vagrant up, you can test with vagrant root@mesos-master. 

1) Load the key_authorization.rb file

```ruby
require_relative './vagrant/key_authorization'
```

2) Add the id_dsa.pub or id_rsa.pub key to the root authorized keys on the remote machines. From [here](https://gist.githubusercontent.com/maxim/dafc3b6da5754419babb/raw/7789793ed7e799dc22e6222c30c6130f34a055e7/key_authorization.rb).

```ruby
authorize_key_for_root config, '~/.ssh/id_dsa.pub', '~/.ssh/id_rsa.pub'
```
    
## It's not fun unless you run it

```
vagrant up
```