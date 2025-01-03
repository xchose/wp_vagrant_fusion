# Vagrant file for default Ubuntu 22 ARM template
# HW configuration in Vagrant
# Soft. config done by ansible
Vagrant.configure("2") do |config|
  BOX_NAME = "bento/ubuntu-22.04-arm64"
  
  # Define the db VM
  config.vm.define "db" do |db|
    db.vm.box = BOX_NAME
    db.vm.hostname = "db"
    db.vm.provider "vmware_desktop" do |v|
      v.vmx["displayName"] = "db"
      v.gui = false
      # Allocate 4 CPUs to ensure the VM has enough processing power for running WordPress and handling multiple simultaneous users
      v.cpus = 4
    end

    # Provision with Ansible
    db.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook_db.yml"
      ansible.extra_vars = {
        "ansible_user" => "vagrant"
      }
    end
  end

  # Define the wp VM
  config.vm.define "wp" do |wp|
    wp.vm.box = BOX_NAME
    wp.vm.hostname = "wp"
    wp.vm.provider "vmware_desktop" do |v|
      v.vmx["displayName"] = "wp"
      v.gui = false
      # Allocate 2 CPUs to ensure the VM has enough processing power for running WordPress
      v.cpus = 2
    end

    # Provision with Ansible
    wp.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook_wp.yml"
      ansible.extra_vars = {
        "ansible_user" => "vagrant"
      }
    end
  end
end