# Icinga2 Ansible Vagrant: master and client node

*No longer maintained: this standalone Icinga2 Vagrant won't be updated anymore, if you want the up to date roles, track them in https://github.com/fiaasco/fiaas*

This project starts with an empty Debian 8.2 vagrant box and uses Ansible to install:
* Icinga2 master on the box icinga2
* Icinga2-classicui and Icingaweb2 on the box icinga2
* Icinga2 client on the box monitored. The box will be added to the master.

## Executing ( vagrant )

The playbook was tested with Ansible 1.9.4. Other versions will probably also work, but if you want to be sure it's easy to setup Ansible with virtualenv for a specific version with the steps below. You don't need the first three steps if you have a working ansible-playbook command in your path.

* virtualenv ./venv/ansible-1.9.4
* source ./venv/ansible-1.9.4/bin/activate
* pip install ansible==1.9.4
* vagrant up --no-provision
* provisioning:
   * OR: vagrant provision
   * OR: ansible-playbook -i inventory/vagrant/ playbooks/icinga.yml -u vagrant -s --ask-pass ( pass = vagrant )
   * OR: ./ansible-vagrant playbooks/icinga.yml and ./ansible-vagrant playbooks/monitored.yml

## Web interface

http://192.168.131.160/icinga2-classicui/
user: icingaadm
pass: icingaadm

http://192.168.131.160/icingaweb2
user: icingaadmin
pass: icingaadmin

All credentials are configured in group_vars/all

## Known issues

* You have to run the monitored play twice to add the inventory of the Icinga Satellite. Icinga2 is not able to update the node config until it's connected and that takes a while.
* The playbooks are not fully idempotent. Send patches if you find a way to fix it. ;-)
