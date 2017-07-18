VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = 'https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/14.04/providers/virtualbox.box'
  config.vm.synced_folder "GettingStarted/", "/home/vagrant/GettingStarted" ,  type: "rsync"
  config.vm.synced_folder "TESTS/", "/home/vagrant/TESTS" ,  type: "rsync"
  config.vm.network :forwarded_port, guest:4444, host:4444
  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.provision "shell", path: "script.sh"
  config.vm.provision 'shell', path: 'always-as-root.sh', run: 'always'

  # machine name (for guest machine console)
  config.vm.hostname = 'selenium'

  config.vm.provider :virtualbox do |vb|
    vb.gui = true
    vb.memory = 1500
    vb.cpus = 2
  end

  config.trigger.before :up do
    run "php repeatHosts.php"
  end

  config.vm.network :public_network

end