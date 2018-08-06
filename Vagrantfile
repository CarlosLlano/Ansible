# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  
  config.vm.define :ansible_master do |ansible_master|
    #definicion de la imagen del SO a utilizar (en este caso Centos7)
    ansible_master.vm.box = "centos/7"
    #Configuracion de una red privada e ip asociada a la maquina
    ansible_master.vm.network :private_network, ip: "192.168.56.101"
    #Configuracion de la cantidad de memoria RAM, numero de cpus y nombre de la maquina virtual
    ansible_master.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "ansible_master" ]
    end    
  end

  config.vm.define :ansible_host do |ansible_host|
    #definicion de la imagen del SO a utilizar (en este caso Centos7)
    ansible_host.vm.box = "centos/7"
    #Configuracion de una red privada e ip asociada a la maquina
    ansible_host.vm.network :private_network, ip: "192.168.56.102"
    #Configuracion de la cantidad de memoria RAM, numero de cpus y nombre de la maquina virtual
    ansible_host.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "ansible_host" ]
    end
    config.vm.provision "shell", inline: <<-SHELL
      #para instalacion de nginx
      yum -y install epel-release
      #para conexion por ssh
      sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config 
      service sshd restart
    SHELL
  end
end
