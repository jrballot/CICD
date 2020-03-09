# -*- mode: ruby -*-
# vi: set ft=ruby :

# Stash test

machines = {
	"scm" => {"memory"=>"4096", "cpus"=>"1", "ip" => "10" },
	"pipeline" => {"memory"=>"4096", "cpus"=>"1", "ip" => "20" },
	"env" => {"memory"=>"2048", "cpus"=>"1", "ip" => "40" },
}

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  
  machines.each do |name,conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.network "private_network", ip: "192.168.88.#{conf["ip"]}"
      machine.vm.hostname = "#{name}.dexter.com.br"
      machine.vm.provider "virtualbox" do |vb|
        vb.cpus = "#{conf["cpus"]}"
	vb.memory = "#{conf["memory"]}"
	vb.name = "#{name}"
	vb.gui = false
      end

    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum install -y epel-release vim
  SHELL

end
