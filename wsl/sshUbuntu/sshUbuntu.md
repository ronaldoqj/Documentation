# OpenVPN on Ubuntu WSL <span align="right">- Documentation.</span>

![This is an image](/images/ssh-ubuntu.jpg)<br>
[:back:](/README.md) [home](/README.md) | **SSH Ubuntu**

<br>

# Guia de Configuração SSH (Ubuntu-WSL) 🐧

Este guia detalha o passo a passo para instalar e configurar o acesso via SSH no subsistema Windows para Linux (WSL), permitindo conexões externas (como via DBeaver ou terminais remotos).

---

## 🛠️ 1. Instalação do Servidor SSH

Rode estes comandos no terminal do Ubuntu. Eles baixarão os arquivos necessários e criarão a pasta /etc/ssh automaticamente:

```bash
sudo apt update
sudo apt install openssh-server
```

---

## 📝 2. Edição do Arquivo de Configuração

Com a instalação finalizada, a pasta e o arquivo terão sido criados. Execute o comando abaixo para editar as permissões:

```bash
sudo nano /etc/ssh/sshd_config
```

### O que fazer dentro do arquivo:
* Procure por **PasswordAuthentication**.
* Mude o valor para **yes**.
* **Dica extra:** Se a linha tiver um **#** na frente (ex: #PasswordAuthentication yes), **apague o #**. O sustenido faz o sistema ignorar aquela linha.

---

## 💾 3. Salve e Reinicie

1.  Pressione **Ctrl + O** e depois **Enter** (para salvar).
2.  Pressione **Ctrl + X** (para sair).
3.  Reinicie o serviço para aplicar as mudanças:

```bash
sudo service ssh restart
```

---

## ✅ Verificando se funcionou

Para ter certeza de que o "caminho" está aberto e o serviço está ativo, digite:

```bash
sudo service ssh status
```

> Deve aparecer algo como: `* sshd is running`.

---

## ⚠️ Detalhe Importante (WSL)

Um detalhe do WSL: toda vez que você fechar o Windows ou reiniciar o computador, o serviço de SSH do Ubuntu pode desligar sozinho. 

**Se o DBeaver parar de conectar**, basta abrir o terminal do Ubuntu e rodar o comando:

```bash
sudo service ssh start
```