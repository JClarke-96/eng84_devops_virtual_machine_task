# Install required plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.local"]
    app.vm.synced_folder ".", "/home/ubuntu/app"
    app.vm.provision "shell", path: "environment/app/provision.sh", privileged: false
    app.vm.provision "shell", inline: 'sudo echo "export DB_HOST=mongodb://192.168.10.101:27017/posts" >> /etc/profile.d/myvars.sh', run: "always"
  end

  config.vm.define "db" do |mongodb|
  	mongodb.vm.box = "ubuntu/xenial64"
  	mongodb.vm.network "private_network", ip: "192.168.10.101"
    mongodb.vm.synced_folder ".", "/home/vagrant/app"
    mongodb.vm.provision "shell", path: "environment/db/provision.sh", privileged: false
  end
  
end
