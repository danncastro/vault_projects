---
description: >-
  Agora que configuramos nosso servidor podemos voltar a nossa estação de
  trabalho e parametrizar o vault para acessar nosso server
---

# Criando secrets no Vault

Para facilitar este processo iremos criar um script para parametrizar nosso cliente

```bash
cd ~/vault/
vim configurevault.sh
```

```vim
#!/bin/bash
export VAULT_ADDR='http://vault.dannielcastro.example:8200'
export VAULT_TOKEN='s.EZE7QYMjfKz6zf5sDHHk6KkL'
```

```bash
chmod +x configurevault.sh
source configurevault.sh
```

Execute _**`vault status`**_ para verificar se o vault foi configurado corretamente.&#x20;

Uma vez configuradas as variáveis de ambiente, podemos interagir com nosso vault server, efetue o login através do comando _**vault login $VAULT\_TOKEN.**_

O Vault trabalha, por padrão com secrets em formato _**kv (key-value).**_&#x20;

{% hint style="success" %}
Para habilitar um secret utilizamos o comando _**vault secrets enable < path >**_ ou _**vault secrets enable -path=< path > < secret\_type >**_
{% endhint %}

{% hint style="info" %}
Existem outras Engines de secrets como Chaves SSH, Tokens AWS ou até mesmo plugins customizados, podemos verificar todos os suportados através da Documentação Oficial.
{% endhint %}

Inicialmente iremos trabalhar com secrets do tipo _**kv**_, para isto, crie o nosso path de armazenamento e liste os secrets disponíveis.

```bash
vault secrets enable -path=blog -description='Segredos do Blog' kv 
vault secrets list
```

{% hint style="success" %}
Para criar um secret em um determinado path, podemos utilizar o comando _**vault kv put < path >/< secret-name > < key >=< value >**_
{% endhint %}

Crie o primeiro secret no nosso vault path _**blog**_

```bash
vault kv put blog/dannielcastro address=dannielcastro.dev
```

Uma mensagem de sucesso informa que o secret foi criado.

`Success! Data written to: blog/dannielcastro`

Utilize o comando _**vault kv list < path >**_ para verificar as chaves existentes no storage.

```bash
vault kv list blog
```

{% hint style="success" %}
Para acessar um secret utilizamos o comando _**vault kv get < path >/< secret >.**_
{% endhint %}

Um secret pode possuir diversos atributos _**key-value**_ bem como subdiretórios, vamos adicionar mais alguns atributos ao nosso path:

```bash
vault kv put blog/caiodelgado/data owner='Danniel Castro' twitter='dannielcastrolz'
```

Listando o nosso path conseguimos verificar que existem agora um secret chamado _**dannielcastro**_ bem como um sub-path _**dannielcastro/**_

{% hint style="success" %}
Para verificar o conteúdo do subpath basta informar o mesmo no comando para listagem.
{% endhint %}

Mesmo que não seja informada a _**`/`**_ final o vault entende que ao utilizar o comando `list` você quer listar um path

Verifique os valores do secret _**data**_
