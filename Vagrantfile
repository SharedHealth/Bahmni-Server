# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "client" do |client|
    client.vm.box = "centos_large"
    client.vm.network :private_network, ip: "192.168.33.18"
    client.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]
    end

    client.vm.provision :ansible do |ansible|
        ansible.verbose = "vvv"
        ansible.extra_vars = {configfile: File.dirname(__FILE__) + "/bd-config/target/bd_config.zip"}

        ansible.playbook = "FreeSHR-Bahmni-Playbooks/bahmni-servers.yml"
        ansible.inventory_path = "./hosts"
        ansible.limit = "all"
        ansible.skip_tags = ["implementation_config"]
    end

    client.vm.provision :ansible do |ansible|
        ansible.verbose = "vvv"
        ansible.extra_vars = {all_omods: File.dirname(__FILE__) + "/openmrs-module-terminology_atomfeed_client/target/openmrs-module-terminology_atomfeed_client-1.0-SNAPSHOT.omod"}
        ansible.playbook = "FreeSHR-Bahmni-Playbooks/tr-feed-clients.yml"
        ansible.inventory_path = "./hosts"
        ansible.limit = "all"
    end
  end

end
