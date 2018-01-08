Vagrant.configure('2') do |config|
	config.vm.define "docker" do |docker|

    #pravega.vm.provision "shell", inline: "apt-get update", privileged: true
    #pravega.vm.provision "shell", inline: "apt-get -y install build-essential linux-headers-`uname -r`", privileged: true
    #pravega.vm.provision "shell", inline: "sudo -E apt-get -y install git zip", privileged: true
    #pravega.vm.provision "file", source: "vagrant", destination: "vagrant"
    #pravega.vm.provision "shell", inline: "chmod 755 vagrant/install-jdk.sh", privileged: true
    #pravega.vm.provision "shell", inline: "vagrant/install-jdk.sh", privileged: true
	    docker.vm.provision "file", source: "docker-compose.yml", destination: "docker-compose.yml"
	    docker.vm.provider :virtualbox do |v, override|

	      override.vm.box = 'ubuntu/trusty64'
	      override.vm.network :private_network, ip: '192.168.50.14', id: :local
	      override.vm.network :public_network
	      v.memory = 6144
	      v.cpus = 2
	    end
	    config.vm.provision "shell", inline: <<-SHELL
	      apt-get install apt-transport-https ca-certificates curl software-properties-common    
	      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"  
    	  apt-get update
    	  apt-get -y install docker-ce
    	  apt-get -y install python-pip
    	  pip install docker-compose
    	  sudo docker run -d -e HOST_IP=192.168.50.14 -p 9090:9090 -p 12345:12345 pravega/pravega:latest standalone
    	SHELL
    end
	  
end