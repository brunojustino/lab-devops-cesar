Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu1804"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.provider "vmware_desktop" do |vmware|
    vmware.vmx["memsize"] = "4096"
    vmware.vmx["numvcpus"] = "2"
  end
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provision "shell" do |s|
    s.inline = <<-SHELL
      sudo apt-get update
      sudo apt-get install -y software-properties-common
      sudo apt-add-repository --yes --update ppa:ansible/ansible
      sudo apt-get install -y ansible
    SHELL
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "ansible/main.yml"
  end
end
