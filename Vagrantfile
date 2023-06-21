# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :web => {
        :box_name => "CentOS-7-x86_64-Vagrant-2004_01",
        :box_version => "0",
		:cpus => 2,
		:memory => 2048,
        :ip_addr => '192.168.56.10',
        },
    
  :log => {
        :box_name => "CentOS-7-x86_64-Vagrant-2004_01",
        :box_version => "0",
		:cpus => 2,
		:memory => 2048,
        :ip_addr => '192.168.56.15',
        }
}

Vagrant.configure("2") do |config|

    config.vm.box_version = "0"
    MACHINES.each do |boxname, boxconfig|
 	config.vm.synced_folder ".", "/vagrant", disabled: true 
        config.vm.define boxname do |box|
  
            box.vm.box = boxconfig[:box_name]
            box.vm.host_name = boxname.to_s
            box.vm.network "private_network", ip: boxconfig[:ip_addr]
            box.vm.provider :virtualbox do |vb|
                            vb.memory = boxconfig[:memory]
                            vb.cpus = boxconfig[:cpus]

       end
            config.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/install.yaml"
            ansible.inventory_path = "ansible/hosts"
			ansible.host_key_checking = "false"
			ansible.limit = "all"
        end
     end
  end
end
