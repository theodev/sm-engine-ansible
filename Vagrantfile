# This guide is optimized for Vagrant 1.7 and above.
# Although versions 1.6.x should behave very similarly, it is recommended
# to upgrade instead of disabling the requirement below.
Vagrant.require_version ">= 1.7.0"

Vagrant.configure(2) do |config|
  
  config.vm.box = "ubuntu/trusty64"
  #config.vm.box = "ubuntu/xenial64"
  
  config.vm.network "forwarded_port", guest: 4040, host: 5040
  config.vm.network "forwarded_port", guest: 8080, host: 9080

  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  #config.ssh.insert_key = false
  #config.ssh.username = "vagrant"
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
	v.cpus = 4
  end

  config.vm.provision :ansible do |ansible|
    ansible.verbose = "vv"
    ansible.inventory_path = "hosts"
    ansible.playbook = "system.yml"
    ansible.extra_vars = {pub_key_file: "~/.ssh/id_rsa.pub"}
    ansible.host_key_checking = false
  end
end
