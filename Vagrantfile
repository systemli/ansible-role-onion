# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 1
  end

  # Ubuntu Precise (12.04 LTS)
  config.vm.define "precise" do |precise|
    precise.vm.hostname = "precise"
    precise.vm.box = "ubuntu/precise64"

    # Ansible.
    precise.vm.provision "ansible" do |ansible|
      ansible.playbook = "vagrant.yml"
      ansible.sudo = true
    end
  end

  # Ubuntu Trusty (14.04 LTS)
  config.vm.define "trusty" do |trusty|
    trusty.vm.hostname = "trusty"
    trusty.vm.box = "ubuntu/trusty64"

    # Ansible.
    trusty.vm.provision "ansible" do |ansible|
      ansible.playbook = "vagrant.yml"
      ansible.sudo = true
    end
  end

  # Debian Wheezy
  config.vm.define "wheezy" do |wheezy|
    wheezy.vm.hostname = "wheezy"
    wheezy.vm.box = "debian/wheezy64"

    # Ansible.
    wheezy.vm.provision "ansible" do |ansible|
      ansible.playbook = "vagrant.yml"
      ansible.sudo = true
    end
  end

  # Debian Jessie
  config.vm.define "jessie", primary: true do |jessie|
    jessie.vm.hostname = "jessie"
    jessie.vm.box = "debian/jessie64"

    # Ansible.
    jessie.vm.provision "ansible" do |ansible|
      ansible.playbook = "vagrant.yml"
      ansible.sudo = true
    end
  end
end
