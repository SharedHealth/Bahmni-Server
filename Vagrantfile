# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "client" do |client|
    client.vm.box = "centos"
    client.vm.network :private_network, ip: "192.168.33.18"
    client.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "3072", "--cpus", "2"]
    end

    client.vm.provision :ansible do |ansible|
        ansible.verbose = "vvv"
        ansible.extra_vars = {config_file: File.dirname(__FILE__) + "/bdshr-config/target/bdshr_config.zip", release_version: "release-5.0"}
        ansible.playbook = "FreeSHR-Bahmni-Playbooks/bahmni-server.yml"
        ansible.inventory_path = "./hosts"
        ansible.limit = "all"
    end

  end

end
