Vagrant.configure("2") do |config|
    config.vm.define "k8s-master" do |master|
        master.vm.box = "bento/ubuntu-20.04"
        master.vm.hostname = "master-node"
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.provider "virtualbox" do |vb|
            vb.memory = 4096
            vb.cpus = 2
        end
    end
    
    (1..2).each do |i|
        config.vm.define "node0#{i}" do |node|
            node.vm.box = "bento/ubuntu-20.04"
            node.vm.hostname = "worker-node0#{i}"
            node.vm.network "private_network", ip: "192.168.50.1#{i}"
            node.vm.provider "virtualbox" do |vb|
                vb.memory = 2048
                vb.cpus = 1
            end
        end
    end
    
    config.vm.define "gitlab" do |gitlab|
        gitlab.vm.box = "bento/ubuntu-20.04"
        gitlab.vm.hostname = "gitlab"
        gitlab.vm.network "private_network", ip: "192.168.50.13"
        gitlab.vm.provider "virtualbox" do |vb|
            vb.memory = 2048
            vb.cpus = 1
        end
    end
    
    config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.groups = {
            "k8s_hosts" => ["k8s-master", "node01", "node02"],
            "k8s_masters" => ["k8s-master"],
            "k8s_workers" => ["node01", "node02"],
            "gitlab_hosts" => ["gitlab"]
        }
        ansible.host_vars = {
            "k8s-master" => {
                "node_ip" => "192.168.50.10"
            },
            "node01" => {
                "node_ip" => "192.168.50.11"
            },
            "node02" => {
                "node_ip" => "192.168.50.12"
            },
            "gitlab" => {
                "node_ip" => "192.168.50.13"
            },
        }
    end
end