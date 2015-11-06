# -*- mode: ruby -*-
# vi: set ft=ruby :
#

DEBIAN82_BOX = "debian82"
DEBIAN82_BOX_URL = "http://stroobl.github.io/boxes/debian-8.2-amd64.box"

Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

  config.vm.define "icinga2" do |v|
    v.vm.box = DEBIAN82_BOX
    v.vm.box_url = DEBIAN82_BOX_URL
    v.vm.hostname = "icinga2"
    v.vm.network :private_network, ip: "192.168.131.160"
    v.vm.network :forwarded_port, guest: 22, host: 2160, id: 'ssh'
    v.vm.provision :ansible do |ansible|
      ansible.inventory_path = "inventory/vagrant/"
      ansible.playbook = "playbooks/icinga.yml"
      ansible.sudo = "true"
      ansible.host_key_checking = "false"
      ansible.limit = 'all'
    end
  end
  config.vm.define "monitored" do |v|
    v.vm.box = DEBIAN82_BOX
    v.vm.box_url = DEBIAN82_BOX_URL
    v.vm.hostname = "monitored"
    v.vm.network :private_network, ip: "192.168.131.161"
    v.vm.network :forwarded_port, guest: 22, host: 2161, id: 'ssh'
    v.vm.provision :ansible do |ansible|
      ansible.inventory_path = "inventory/vagrant/"
      ansible.playbook = "playbooks/monitored.yml"
      ansible.sudo = "true"
      ansible.host_key_checking = "false"
      ansible.limit = 'all'
    end
  end
end
