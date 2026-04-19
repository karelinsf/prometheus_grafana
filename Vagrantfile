
VAGRANTFILE_API_VERSION = "2"
#ENV['VAGRANT_SERVER_URL'] = 'http://vagrant.elab.pro'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  #config.vm.provider = 'virtualbox'
  
  
  config.vm.define "promserver" do | ps |
    ps.vm.box = 'ubuntu/jammy64'
    ps.vm.host_name = "promserver"
    ps.vm.network "public_network", bridge: "enp7s0"
    ps.vm.network "private_network", ip: "192.168.56.10"
       ps.vm.provider :virtualbox do |res|

          res.customize ["modifyvm", :id, "--cpus", "2"]
          res.customize ["modifyvm", :id, "--memory", "2000"]
       end

  end

  config.vm.define "net1" do | n1 |
    n1.vm.box= 'ubuntu/jammy64'
    n1.vm.host_name = "net1"

    n1.vm.network "private_network", ip: "192.168.56.11"
    
      n1.vm.provider :virtualbox do |res|

        res.customize ["modifyvm", :id, "--cpus", "2"]
        res.customize ["modifyvm", :id, "--memory", "2000"]
      end

  end

  config.vm.define "net2" do | n2 |
    n2.vm.box= 'ubuntu/jammy64'
    n2.vm.host_name = "net1"

    n2.vm.network "private_network", ip: "192.168.56.12"
    
      n2.vm.provider :virtualbox do |res|

        res.customize ["modifyvm", :id, "--cpus", "2"]
        res.customize ["modifyvm", :id, "--memory", "2000"]
      end

  end

  config.vm.provision "ansible" do |ansible|
    ansible.groups = {
      "prometheus-server" => ["promserver"],
      "net" => ["net1", "net2"],
    }
    ansible.playbook = "playbook.yml"
    ansible.compatibility_mode = "2.0"
  end

end