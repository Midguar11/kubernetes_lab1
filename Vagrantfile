Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-18.04"
    config.vm.hostname = "minikube"
    config.vm.network "private_network", ip: "120.16.1.10"
    config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", 4096]
      v.customize ["modifyvm", :id, "--cpus", 2]
    end
  end