# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

ENV['ANSIBLE_ROLES_PATH'] = "#{File.dirname(__FILE__)}/../"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 1
  end

  # Ubuntu Xenial (16.04 LTS)
  config.vm.define "xenial" do |xenial|
    xenial.vm.hostname = "xenial64"
    xenial.vm.box = "ubuntu/xenial64"

    # Ansible.
    xenial.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "vagrant.yml"
      ansible.become = true
    end
  end

  # Ubuntu Bionic (18.04 LTS)
  config.vm.define "bionic" do |bionic|
    bionic.vm.hostname = "bionic64"
    bionic.vm.box = "ubuntu/bionic64"

    # Ansible.
    bionic.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "vagrant.yml"
      ansible.become = true
    end
  end

  # Debian Wheezy
  config.vm.define "jessie" do |jessie|
    jessie.vm.hostname = "jessie64"
    jessie.vm.box = "debian/jessie64"

    # Ansible.
    jessie.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "vagrant.yml"
      ansible.become = true
    end
  end

  # Debian stretch
  config.vm.define "stretch", primary: true do |stretch|
    stretch.vm.hostname = "stretch64"
    stretch.vm.box = "debian/stretch64"

    # Ansible.
    stretch.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "vagrant.yml"
      ansible.become = true
    end
  end
end
