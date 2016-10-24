# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

MASTER_MEMORY=1024
AGENT_MEMORY=1024

RANCH_MASTER_ADDRESS="172.19.8.100"
# Boxes are configured at 101, 102 and so on
RANCH_SUBNET="172.19.8"


RANCHER_SERVER_DOMAIN_NAME="ranch-svr.infracloud.io"
RANCHER_CLIENT_DEF="ranch-def.infracloud.io"
RANCHER_CLIENT_K8S="ranch-k8s.infracloud.io"


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	config.vm.define "ranch_server" do |rserver|
		rserver.vm.box = "ubuntu/trusty64"
		rserver.vm.network "private_network", ip: "#{RANCH_MASTER_ADDRESS}"	
		rserver.vm.hostname = "#{RANCHER_SERVER_DOMAIN_NAME}"
		rserver.vm.provider :virtualbox do |vba|
			vba.customize ["modifyvm", :id, "--memory", MASTER_MEMORY]
		end
		rserver.vm.provision "shell", inline: "wget -qO- https://get.docker.com/ | sh"			
		rserver.vm.provision "shell", inline: "sudo docker run -d --restart=always -p 8080:8080 rancher/server"		
	end

	config.vm.define "ranch_c_default" do |rclient|
		rclient.vm.box = "ubuntu/trusty64"
		rclient.vm.network "private_network", ip: "#{RANCH_SUBNET}.101"
		rclient.vm.hostname = "#{RANCHER_CLIENT_DEF}"
		rclient.vm.provider :virtualbox do |vba|
			vba.customize ["modifyvm", :id, "--memory", AGENT_MEMORY]
		end
		rclient.vm.provision "shell", inline: "wget -qO- https://get.docker.com/ | sh"		
		# K8S works with slightly older version of Docker hence downgrading
		rclient.vm.provision "shell", inline: "sudo apt-get install docker-engine=1.10.3-0~trusty"		
	end

	config.vm.define "ranch_c_k8s" do |rclient|
		rclient.vm.box = "ubuntu/trusty64"
		rclient.vm.network "private_network", ip: "#{RANCH_SUBNET}.102"
		rclient.vm.hostname = "#{RANCHER_CLIENT_K8S}"
		rclient.vm.provider :virtualbox do |vba|
			vba.customize ["modifyvm", :id, "--memory", AGENT_MEMORY]
		end
		rclient.vm.provision "shell", inline: "wget -qO- https://get.docker.com/ | sh"
		# K8S works with slightly older version of Docker hence downgrading
		rclient.vm.provision "shell", inline: "sudo apt-get install docker-engine=1.10.3-0~trusty"		
	end

end
