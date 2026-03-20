# OpenVPN on Ubuntu WSL <span align="right">- Documentation.</span>

![This is an image](/images/dbeaver.jpg)<br>
[:back:](/README.md) [home](/README.md) | **Dbeaver SSH Conection**

<br>

# Configuração de Conexão no DBeaver (via SSH Tunnel) 🐘

Este guia explica como configurar o DBeaver no Windows para se conectar a um banco de dados utilizando o Ubuntu-WSL como ponte (túnel SSH).

---

## 🛠️ Passo a Passo no DBeaver

Com o servidor SSH já ativo e rodando no seu Ubuntu, siga exatamente esta ordem de configuração:

### 1. Na aba "Principal" (Main)
Nesta aba, você preenche os dados como se estivesse dentro do servidor de banco de dados:

* **Host:** O IP ou Hostname do banco de dados (ex: `10.0.1.50` ou `db.empresa.com`).
* **Porta:** A porta padrão do banco (ex: `5432` para Postgres, `3306` para MySQL).
* **Autenticação:** O usuário e a senha do **Banco de Dados**.

---

### 2. Na aba "SSH"
Aqui é onde configuramos o Ubuntu-WSL para servir de "ponte":

* **Checkmark:** Marque a opção **"Use SSH Tunnel"**.
* **SSH Host:** `localhost`
* **Port:** `22`
* **User Name:** `[Linux Username]`
* **Authentication Method:** `Password`
* **Password:** `[Linux password]`

---

## 💡 Dica de Ouro: Erro de "Connection Refused"

Se ao tentar conectar o DBeaver exibir um erro de "Connection Refused", o Windows pode estar com dificuldade de localizar o `localhost` do WSL. 

Nesse caso, você deve trocar o **SSH Host** de `localhost` para o IP real do Ubuntu. Para descobrir esse IP, rode o seguinte comando no terminal do Ubuntu:

```bash
hostname -I | awk '{print $1}'
```

> **Ação:** Copie o número que aparecer (algo como `172.x.x.x`) e cole no campo **SSH Host** do DBeaver.

---

## ⚠️ Lembrete de Execução
Se a conexão falhar amanhã, verifique se o serviço SSH está ativo no Ubuntu com o comando:
`sudo service ssh start`
