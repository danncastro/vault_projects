---
description: >-
  Para armazenar os dados do vault precisaremos de um servidor, para isto iremos
  utilizar um Ubuntu Server através do Vagrant.
---

# Instalar Vault Server

Você pode utilizar qualquer máquina virtual que quiser, basta seguir para a próxima seção caso não queira utilizar o Vagrant.

## **Vagrantfile para o vault server**

Vamos criar um diretório para armazenar o conteúdo do _**`Vagrantfile`**_ e popula-lo com as configurações para subir o ambiente.

Também é possível rodar o _**vault server no modo dev (localmente)**_ através do comando _**`vault server-dev.`**_

{% hint style="danger" %}
A utilização do _**`vault server-dev`**_ não é indicada em ambientes de produção.
{% endhint %}

```sh
mkdir ~/vault
cd ~/vault
vim Vagrantfile
```

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby  :

Vagrant.configure("2") do |config|
    config.vm.box_check_update = false
    config.vm.boot_timeout = 600
    config.vm.define "vault" do |machine|
        machine.vm.box = "ubuntu/bionic64"
        machine.vm.hostname = "vault.dannielcastro.example"
        machine.vm.network "private_network", ip: "10.10.10.10"
        machine.vm.provider "virtualbox" do |vb|
            vb.name = "vault"
            vb.memory = "1024"
            vb.cpus = "1" 
            vb.customize ["modifyvm", :id, "--groups", "/iac"]
        end
    end
end
```

```sh
vagrant up
```

Adicione a entrada do vault no arquivo hosts para que o acesso ao mesmo fique mais fácil.

```sh
sudo sh -c "echo '10.10.10.10 vault.dannielcastro.example' >> /etc/hosts"
```
