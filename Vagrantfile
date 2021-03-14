# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

prefix = "192.168.122"
infra = {
  "main"  => { :ip => "#{prefix}.10", :cpus => 2, :mem => 4096 },
  "k8s-1" => { :ip => "#{prefix}.11", :cpus => 1, :mem => 2048 },
  "k8s-2" => { :ip => "#{prefix}.12", :cpus => 1, :mem => 2048 },
  "k8s-3" => { :ip => "#{prefix}.13", :cpus => 1, :mem => 2048 },

}
 
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  infra.each_with_index do |(hostname, info), index|

    config.vm.define hostname do |cfg|
      cfg.vm.box = "centos/7"
      cfg.vm.network :public_network,
          :ip => "#{info[:ip]}",
          :dev => "virbr0",
          :mode => "bridge",
          :type => "bridge"      

      cfg.vm.provider :virtualbox do |vb|

        vb.memory = "#{info[:mem]}"
        vb.cpus   = "#{info[:cpus]}"
        
      cfg.vm.provision "bootstrap", type: "shell" do |s|
          s.inline = "sudo yum update -y"
        end
      
      end # end provider
    end # end config
  end # end infra
end



