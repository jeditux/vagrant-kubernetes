Vagrant.configure("2") do |config|
    config.vm.define "master" do |master|
        master.vm.box = "bento/ubuntu-20.04"
        master.vm.hostname = "master-node"
        master.vm.network "private_network", ip: "10.0.0.10"
        master.vm.provider "virtualbox" do |vb|
            vb.memory = 4096
            vb.cpus = 2
        end
    end
    
    (1..2).each do |i|
        config.vm.define "node0#{i}" do |node|
            node.vm.box = "bento/ubuntu-20.04"
            node.vm.hostname = "worker-node0#{i}"
            node.vm.network "private_network", ip: "10.0.0.1#{i}"
            node.vm.provider "virtualbox" do |vb|
                vb.memory = 2048
                vb.cpus = 1
            end
        end
    end
    
    config.vm.define "gitlab" do |gitlab|
        gitlab.vm.box = "bento/ubuntu-20.04"
        gitlab.vm.hostname = "gitlab"
        gitlab.vm.network "private_network", ip: "10.0.0.13"
        gitlab.vm.provider "virtualbox" do |vb|
            vb.memory = 2048
            vb.cpus = 1
        end
    end
end