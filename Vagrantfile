required_plugins = %w( vagrant-vbguest )

required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|

  config.vm.box = "centos7"
  config.vm.box_url = "centos7.box"
  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 443, host: 8443, host_ip: "127.0.0.1"

  # config.vm.provider "virtualbox" do |vb|
  #   vb.memory = "1024"
  # end


  # Aviod replacing insecure key
  # It leads to permission error
  # Vagrant insecure key detected. Vagrant will automatically replace.
  # /home/vagrant/.ssh/authorized_keys: Permission denied
  config.ssh.insert_key = false

  config.vm.provision "ansible", run: "always" do |ansible|
    ansible.playbook = ENV['PLAYBOOK']
  end

end
