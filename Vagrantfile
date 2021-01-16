$vm_box = "centos/7"
$vm_box_version = "1905.1"
$k3s_ip = "192.168.77.100"

Vagrant.configure("2") do |config|
	config.vm.define "k3s", primary: true do |k3s|
		k3s.vm.box = $vm_box
		k3s.vm.box_version = $vm_box_version

		k3s.vm.box_check_update = false
	  
		k3s.vm.hostname = "k3s"
	  
		k3s.vm.network "private_network", ip: $k3s_ip

		k3s.vm.provider "virtualbox" do |vb|
			vb.name = "k3s"
			vb.memory = 4096 #$vm_memory
			vb.cpus = 2 #$vm_cpus
			vb.gui = false
		end

		k3s.vm.provision "shell", inline: <<-SHELL
			#update to latest packages
			yum -y update

			#turn off firewall
			systemctl disable firewalld && systemctl stop firewalld

			# install required packages
			yum install -y git sed sshpass ntp wget net-tools bind-utils bash-completion

			#install k3s
			#export INSTALL_K3S_VERSION=v1.19.5+k3s2
			export INSTALL_K3S_VERSION=v1.19.7+k3s1
			#export INSTALL_K3S_VERSION=v1.20.0+k3s2
			curl -sfL https://get.k3s.io | sh -
		SHELL
	end
end
