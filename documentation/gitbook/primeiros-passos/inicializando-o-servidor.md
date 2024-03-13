---
description: >-
  Agora que já parametrizamos o Banco de Dados e o Vault Server, podemos
  inicializar o servidor através do comando vault operator init
---

# Inicializando o servidor

```sh
vault operator init 
```

## Output:

```sh
Unseal Key 1: F9Yo6vPumyQfuhTlTqcgkJhG3s02oeKJ6hNmkDKzItDE
Unseal Key 2: tuRLZjNOIv2DPO+TD3P3h9Gv1QQSL8rsFhjAe5q4CheH
Unseal Key 3: qA1TZ5J9iE2V3R6y/5DJh0i29MPTnGLsF/hvia2sOVAS
Unseal Key 4: GkDqxi6PbUj11bpQRJgJS9Fqebv0rxa+nYZCWcuZi0xG
Unseal Key 5: yMNs+Qh+LvOxav6ChiG3/uXhRQWRh1CY1vh1vUXqLtlt

Initial Root Token: s.EZE7QYMjfKz6zf5sDHHk6KkL

Vault initialized with 5 key shares and a key threshold of 3. Please securely
distribute the key shares printed above. When the Vault is re-sealed,
restarted, or stopped, you must supply at least 3 of these keys to unseal it
before it can start servicing requests.

Vault does not store the generated master key. Without at least 3 key to
reconstruct the master key, Vault will remain permanently sealed!

It is possible to generate new unseal keys, provided you have a quorum of
existing unseal keys shares. See "vault operator rekey" for more information.
```

Após inicializar o vault dois dados muito importantes são exibidos, a _**unseal key**_ e a _**initial root token.**_

{% hint style="warning" %}
_**ATENÇÃO:**_ Estes dados serão exibidos uma única vez  pelo Vault, guarde as **unseal key** em um local seguro, de preferencia cada chave em um local diferente, uma vez que estas chaves serão responsáveis pelo desbloqueio do cofre.
{% endhint %}

{% hint style="info" %}
Todo servidor do Vault inicializa em **sealed state** (estado lacrado/selado).
{% endhint %}

Neste ponto o Vault consegue acessar o storage fisicamente porém não consegue desencriptar os dados.

* Precisaremos das unseal Keys para ensinar o Vault a descriptografar os dados.

O processo de unseal deve ser realizado a cada momento que o vault iniciar e pode ser realizado pela CLI ou via API.&#x20;

{% hint style="success" %}
Note que a mensagem **Vault initialized with 5 key** **shares and a key threshold of 3** foi exibida na inicialização, o que significa que são necessárias 3 das 5 chaves para o processo de unseal.
{% endhint %}
