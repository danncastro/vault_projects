---
description: >-
  Como configuramos nosso storage backend para o mysql precisamos fazer a
  instalação do mesmo, iremos utilizar o MariaDB que é a versão open source do
  mysql e criar um usuário e o banco.
---

# Criando o Banco de Dados

```sh
sudo apt update
sudo apt install mariadb-client mariadb-server -y
mysql -u root
```

```sql
> CREATE DATABASE vault;
> CREATE USER 'vaultuser'@'localhost' IDENTIFIED BY 'dannielcastro.dev';
> GRANT ALL PRIVILEGES ON vault.* TO 'vaultuser'@'localhost';
```

Em ambientes de produção lembre-se de executar o comando _**`mysql_secure_installation`**_ para aumentar a segurança do banco de dados.
