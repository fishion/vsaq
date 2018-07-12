# -*- mode: ruby -*-
# vi: set ft=ruby :

# Basic Configuration
hostname      = 'vasq'
box           = 'ubuntu/xenial64'
cpus          = 4
ram           = 2048
guest_ip      = "192.168.33.17"

Vagrant.configure(2) do |config|
  config.vm.box = box
  config.vm.hostname = hostname

  #####
  # VirtualBox-specific config 

  config.vm.provider 'virtualbox' do |vb|
    vb.customize [
      'modifyvm', :id,
      "--uartmode1", "disconnected",
      '--memory', ram,
      '--cpus', cpus
    ]
  end
  
  #####
  # Networking

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: guest_ip

  #####
  # Provisioning

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = ".ansible/playbook.yml"
    ansible.host_vars = {
      "default" => {
        "ansible_python_interpreter" => "/usr/bin/python3"
      }
    }
  end

end
