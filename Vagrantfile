# -*- mode: ruby -*-
# vi: set ft=ruby :

system("
    if [ #{ARGV[0]} = 'up' ]; then
        echo 'You are doing vagrant up and can execute your script'
        ansible-galaxy install -r requirements.yml --force
    fi
")

VAGRANT_VERSION = 2
Vagrant.configure(VAGRANT_VERSION) do |config|
	config.ssh.forward_agent = true
	config.vm.provider "virtualbox" do |v|
		v.memory = 2048
	end
	config.vm.define "pgbouncer" do |server|
		server.vm.box = "ubuntu/trusty64"
		#server.vm.box = "hashicorp/precise64"
		server.vm.hostname = "pgbouncer"
		server.vm.provision :ansible do |ansible|
			ansible.playbook = "test.yml"
		end
	end
end
