Vagrant.configure('2') do |config|
	config.vm.box = 'ubuntu/xenial64'
	config.vm.synced_folder '.', '/vagrant', disabled: true
		config.vm.provider :virtualbox do |v|
    		v.memory = 512
    		v.cpus = 1
	end
  # ansible vm
  config.vm.define 'ansiblevm' do |ansiblevm|
	ansiblevm.vm.hostname = 'ansiblevm.local'
	ansiblevm.vm.network :private_network, ip: '192.168.11.11'
	ansiblevm.vm.synced_folder '.', '/home/ubuntu/ansible', mount_options: ['dmode=700,fmode=600']
	ansiblevm.vm.provision 'ansible', type: 'shell', path: 'ansible-setup.sh'
  end
  # ubuntu node vm
  config.vm.define 'ubuntuhost' do |ubuntuhost|
    	ubuntuhost.vm.hostname = 'ubuntuhost.local'
    	ubuntuhost.vm.network :private_network, ip: '192.168.11.12'
   	ubuntuhost.vm.provision 'python', type: 'shell', inline: 'apt-get install python-minimal -y'
	ubuntuhost.vm.provision 'aptitude', type: 'shell', inline: 'apt-get install aptitude -y'
  end
end