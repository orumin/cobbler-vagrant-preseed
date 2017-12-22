VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "geerlingguy/centos7"

  config.vm.network "private_network", ip: "192.168.33.11"

  if ENV['VAGRANT_BRIDGE']
    interfaces = %x(VBoxManage list bridgedifs)
    re         = /Name: +(.*#{ENV['VAGRANT_BRIDGE']}.*)/

    if interfaces =~ re
      config.vm.network :public_network, bridge: $1, ip: "192.168.151.3"
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.inventory_path = "provisioning/hosts"
    ansible.limit = 'all'
  end
  
end

# vim: set ft=ruby:
