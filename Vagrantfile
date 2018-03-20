#-----  Vagrant file : create N Web servers behind nginx load balancer 


NUMBER_OF_NODES = 2 # N

Vagrant.configure("2") do |config|

  groups = {
    "webservers" => ["web[1:#{NUMBER_OF_NODES}]"],
    "loadbalancers" => ["load_balancer"],
    "all_groups:children" => ["webservers","loadbalancers"]
  }

  # create the N webnodes  
  (1..NUMBER_OF_NODES).each do |i|
    config.vm.define "web#{i}" do |node|
        node.vm.box = "bento/ubuntu-16.04"
        node.vm.hostname = "web#{i}"
        node.vm.network :private_network, ip: "10.10.10.2#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "808#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = 256
        end
      

      if i == NUMBER_OF_NODES
          node.vm.provision "ansible" do |ansible|
            ansible.playbook = "web_playbook.yml"
            ansible.sudo = true
            ansible.limit = "all"
            ansible.groups = groups
          end
        end

      end
    end


    # create nginx load balancer
    config.vm.define "load_balancer" do |lb_config|
        lb_config.vm.box = "bento/ubuntu-16.04"
        lb_config.vm.hostname = "lb"
        lb_config.vm.network :private_network, ip: "10.10.10.11"
        lb_config.vm.network "forwarded_port", guest: 80, host: 8011
        lb_config.vm.provider "virtualbox" do |vb|
          vb.memory = 256
        end
        lb_config.vm.provision "ansible" do |ansible|
          ansible.playbook = "loadbalancer_playbook.yml"
          ansible.sudo = true
          ansible.groups = groups
        end
    end
end

