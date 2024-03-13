---
description: Primeiramente precisamos instalar o cliente do vault na nossa workstation.
---

# Instalação Vault Client

No Linux podemos efetuar o download e instalação através do comando:

```shell
  cd /tmp
  curl https://releases.hashicorp.com/vault/1.4.0/vault_1.4.0_linux_amd64.zip -o vault.zip
  unzip vault.zip
  sudo mv vault /usr/local/bin
```

Ao executar o comando _**`vault --version`**_ deve ser exibida a versão do cliente do vault, informando que a instalação foi efetuada com sucesso.

Podemos também instalar o recurso de autocomplete **(atualmente funcionando apenas nos terminais `bash, zsh e fish`)** que irá facilitar nosso trabalho com o Vault através do comando _**`vault-autocomplete-install`**_.
