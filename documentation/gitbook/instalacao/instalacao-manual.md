---
description: Vamos acessar o servidor para instalar o vault server.
---

# Instalação manual

```sh
cd ~/vault
vagrant ssh
```

Agora que estamos conectados no servidor podemos instalar o Vault.

```sh
sudo su -
cd /tmp
curl https://releases.hashicorp.com/vault/1.4.0/vault_1.4.0_linux_amd64.zip -o vault.zip
unzip vault.zip
mv vault /usr/local/bin
```

Precisamos também dar ao _**Vault**_ o acesso ao _**syscall mlock (previne a memória de ser jogada para o swap)**_ sem rodar o processo como root e criar o usuário vault para rodar o serviço.

```shell
setcap cap_ipc_lock=+ep /usr/local/bin/vault
useradd --system --home /etc/vault.d --shell /bin/false vault
```

Agora podemos criar os arquivos de configuração responsáveis por parametrizar o vault server.

```sh
mkdir -p /etc/vault.d
touch /etc/vault.d/config.hcl
chown -R vault:vault /etc/vault.d
chmod 600 /etc/vault.d/config.hcl
vim /etc/vault.d/config.hcl
```

```vim
storage "mysql" {
  username = "vaultuser"
  password = "dannielcastro.dev"
  database = "vault"
}

listener "tcp" {
  address     = "10.10.10.10:8200"
  tls_disable = 1
}
```
