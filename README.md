# Projeto Cesar School Devops

## Sobre

Automatizar a criação de um servidor NGINX

## Stack

- Vagrant
- Ansible
- Docker
- Nginx

## Ansible no windows

O Ansible não roda no windows. Então para o Ansible funcionar, é necessário instala-lo dentro da VM criada pelo Vagrant. Para fazer isso usamos o módulo `ansible_local` em vez do módulo `ansible`

```sh
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
```