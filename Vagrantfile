Vagrant.configure("2") do |config|

  (1..2).each do |i|
    config.vm.define "mongo_config_#{i}" do |set_config|
        set_config.vm.hostname = "mongo-config-#{i}"
        set_config.vm.box = "bento/ubuntu-18.04"
        set_config.vm.network "private_network", ip: "192.168.212.#{i+1}"
        set_config.vm.provider "virtualbox" do |vb|
          vb.name = "mongo-config-#{i}"
          vb.gui = false
          vb.memory = "1024"
        end
        set_config.vm.provision "shell", path: "provision/config-server-#{i}.sh", privileged: false
    end
  end

  (1..3).each do |i|
    config.vm.define "mongo_shard_#{i}" do |set_shard|
        set_shard.vm.hostname = "mongo-shard-#{i}"
        set_shard.vm.box = "bento/ubuntu-18.04"
        set_shard.vm.network "private_network", ip: "192.168.212.#{3+i}"
        set_shard.vm.provider "virtualbox" do |vb|
          vb.name = "mongo-shard-#{i}"
          vb.gui = false
          vb.memory = "1024"
        end
        set_shard.vm.provision "shell", path: "provision/mongo-shard-#{i}.sh", privileged: false
    end
  end

  config.vm.define "mongo_router" do |set_router|
    set_router.vm.hostname = "mongo-router"
    set_router.vm.box = "bento/ubuntu-18.04"
    set_router.vm.network "private_network", ip: "192.168.212.7"
    set_router.vm.provider "virtualbox" do |vb|
      vb.name = "mongo-router"
      vb.gui = false
      vb.memory = "1024"
    end
    set_router.vm.provision "shell", path: "provision/router.sh", privileged: false
  end

end