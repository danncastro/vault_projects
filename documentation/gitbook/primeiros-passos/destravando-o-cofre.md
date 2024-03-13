---
description: >-
  Para destravar o cofre (unseal the vault ) podemos executar o comando vault
  operator unseal e digitar uma das chaves.
---

# Destravando o Cofre

{% hint style="info" %}
Note que o _**Unseal Progress**_ é listado como _**1/3**_ ou seja, digitamos uma de 3 chaves necessárias para destravar o cofre e o mesmo encontra-se em estado de _**Sealed.**_ Repita o passo mais duas vezes com chaves diferentes para destravar o cofre.
{% endhint %}

Uma vez que o cofre for destravado, a mensagem de exibição será _**Sealed false**_ o que significa que podemos começar a utilizar nosso vault.

Finalmente podemos autenticar com o usuário root criado inicialmente.&#x20;

{% hint style="success" %}
Para isto execute o comando _**vault login**_ somado do token informado no processo de execução do comando _**vault operator init.**_
{% endhint %}
