Vagrant.configure("2") do |config|
  # Base VM OS configuration.
  config.vm.box = "CentOS-7-x86_64-Vagrant-2004_01"
  config.vm.box_version = "0"

  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 2
 
end

  # Define two VMs with static private IP addresses.
  boxes = [
    { :name => "web",
      :ip => "192.168.56.10",
    },
    { :name => "log",
      :ip => "192.168.56.15",
    }
  ]
  # Provision each of the VMs.
  boxes.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.hostname = opts[:name]
      config.vm.synced_folder ".", "/vagrant", disabled: true
      config.vm.network "private_network", ip: opts[:ip]

      if opts[:name] == boxes.last[:name] 
        config.vm.provision "ansible" do |ansible|
          ansible.playbook = "ansible/syslog/ansible/install.yaml"
          ansible.limit = "all"
#          ansible.verbose = "true"
        end
      end
   end
  end
end
