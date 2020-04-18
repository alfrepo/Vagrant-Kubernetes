# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
    # The most common configuration options are documented and commented below.
    # For a complete reference, please see the online documentation at
    # https://docs.vagrantup.com.

    # Every Vagrant development environment requires a box. You can search for
    # boxes at https://vagrantcloud.com/search.
    config.vm.box = "geerlingguy/ubuntu1804"

    PATH_VAGRANT_PROJECT=File.dirname(__FILE__)

    config.ssh.insert_key = false

    # forwarding ports
    # config.vm.network "forwarded_port", guest: 30000, host: 30000 # k8s demo app
    # config.vm.network "forwarded_port", guest: 3000, host: 3000, protocol: "tcp" # node.js apps
    # config.vm.network "forwarded_port", guest: 3000, host: 3000, protocol: "udp" # node.js apps
    # config.vm.network "forwarded_port", guest: 4200, host: 4200, protocol: "tcp" # node.js apps
    # config.vm.network "forwarded_port", guest: 4200, host: 4200, protocol: "udp" # node.js apps
    # config.vm.network "forwarded_port", guest: 5000, host: 5000, protocol: "tcp" # demo auth0 apps
    # config.vm.network "forwarded_port", guest: 5000, host: 5000, protocol: "udp" # demo auth0 apps
    # config.vm.network "forwarded_port", guest: 8000, host: 8000, protocol: "tcp" # dev dynamo DB
    # config.vm.network "forwarded_port", guest: 8000, host: 8000, protocol: "udp" # dev dynamo DB
	# config.vm.network "forwarded_port", guest: 8001, host: 8001, protocol: "tcp" # dev dynamo DB
	# config.vm.network "forwarded_port", guest: 8001, host: 8001, protocol: "udp" # dev dynamo DB
	# config.vm.network "forwarded_port", guest: 8443, host: 8443, protocol: "tcp" # dev dynamo DB
	# config.vm.network "forwarded_port", guest: 8443, host: 8443, protocol: "udp" # dev dynamo DB
    # config.vm.network "forwarded_port", guest: 389, host: 389, protocol: "tcp" # demo auth0 apps
    # config.vm.network "forwarded_port", guest: 389, host: 389, protocol: "udp" # demo auth0 apps
    # config.vm.network "forwarded_port", guest: 636, host: 636, protocol: "tcp" # demo auth0 apps
    # config.vm.network "forwarded_port", guest: 636, host: 636, protocol: "udp" # demo auth0 apps
	# config.vm.network "forwarded_port", guest: 5432, host: 5432 # postgres apps
	# config.vm.network "forwarded_port", guest: 8002, host: 8002 # postgres DB admin ui
	# config.vm.network "forwarded_port", guest: 8003, host: 8003 # free
	# config.vm.network "forwarded_port", guest: 8004, host: 8004 # free
	# config.vm.network "forwarded_port", guest: 8005, host: 8005 # free
	# config.vm.network "forwarded_port", guest: 8006, host: 8006 # free
    # config.vm.network "forwarded_port", guest: 8007, host: 8007 # free
    # config.vm.network "forwarded_port", guest: 8008, host: 8008 # free
	# config.vm.network "forwarded_port", guest: 8009, host: 8009 # free
    # config.vm.network "forwarded_port", guest: 3300, host: 3300, protocol: "tcp" # For ssh tunnel
    # config.vm.network "forwarded_port", guest: 3300, host: 3300, protocol: "udp" # For ssh tunnel
    # config.vm.network "forwarded_port", guest: 8888, host: 8888 # chronograph
    # config.vm.network "forwarded_port", guest: 8092, host: 8092 # telegraph
    # config.vm.network "forwarded_port", guest: 8125, host: 8125 # telegraph
    # config.vm.network "forwarded_port", guest: 8094, host: 8094 # telegraph
    # config.vm.network "forwarded_port", guest: 9092, host: 9092 # kapacitor
    # config.vm.network "forwarded_port", guest: 8086, host: 8086 # influxdb

    # make the root disk available
    config.vm.synced_folder "c:/", "//mnt/c/"

    config.vm.provider "virtualbox" do |v|
        v.memory = 8112
        v.cpus = 4
    end


    # Use shell script to provision
    config.vm.provision "shell", inline: <<-SHELL


    # kubectl
    # https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux
    curl -LfsO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
    chmod +x ./kubectl
    sudo mv ./kubectl /usr/local/bin/kubectl




    # DOCKER
    # for --driver=none minikube installation without VM

    # Install packages to allow apt to use a repository over HTTPS:
    sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common





    # Add Docker’s official GPG key:
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    # add the docker stable repository
    sudo add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"

    # update
    apt-get update -y

    # install docker
    apt-get install -y docker-ce


    sudo systemctl daemon-reload
    sudo systemctl restart docker






    # add docker compose
    curl -fsSL "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-Linux-x86_64" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose





    # MINIKUBE

    curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    chmod +x minikube

    mkdir -p /usr/local/bin/
    install minikube /usr/local/bin/

    # requirements for k8s
    sudo apt-get install -y conntrack



    # Helm
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
    chmod 700 get_helm.sh
    ./get_helm.sh



    echo "to start minikube call -  minikube start --driver=none"

    SHELL

end
