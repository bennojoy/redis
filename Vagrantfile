# -*- mode: ruby -*-
# vi: set ft=ruby :

MEMORY_DEFAULT = 512

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "redis"

  config.vm.provider :virtualbox do |v|
    v.memory = MEMORY_DEFAULT
  end

  config.vm.provider :vmware_fusion do |v|
    v.vmx["memsize"] = MEMORY_DEFAULT
  end

  config.vm.provision :shell, inline: "apt-get purge -qq -y --auto-remove chef puppet"
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "test.yml"
  end
end
