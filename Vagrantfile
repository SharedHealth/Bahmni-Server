# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define "client" do |client|
    client.vm.box = "centos"
    client.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-65-x64-virtualbox-puppet.box"
    client.vm.network :private_network, ip: "192.168.33.18"
    client.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]
    end

    print "Enter go server username: "
    username = STDIN.gets
    print "enter go server password "
    password = STDIN.gets

    client.vm.provision :ansible do |ansible|
        ansible.verbose = "vvv"
        ansible.extra_vars = {config: File.dirname(__FILE__) + "/bd-config/target/bd_config.zip", go_admin: username, go_password: password}
        ansible.skip_tags = ["go-deploy"]
        ansible.playbook = "FreeSHR-Playbooks/bahmni-servers.yml"
        ansible.inventory_path = "./hosts"
        ansible.limit = "all"
    end

    client.vm.provision :ansible do |ansible|
        ansible.verbose = "vvv"
        ansible.extra_vars = {all_omods: File.dirname(__FILE__) + "/openmrs-module-terminology_atomfeed_client/target/openmrs-module-terminology_atomfeed_client-1.0-SNAPSHOT.omod"}
        ansible.playbook = "FreeSHR-Playbooks/tr-feed-clients.yml"
        ansible.inventory_path = "./hosts"
        ansible.limit = "all"
    end
  end

end
