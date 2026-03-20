# WSL <span align="right">- Instalação e documentação de comandos.</span>

![This is an image](/images/wsl-header.jpg)<br>
[:back:](/README.md) [home](/README.md) | **WSL**

<br>

### 🚀 Install
> ```ruby
> $ wsl --install
> ```

> **Obs:** Caso ao executar o comando acima seja exibido o helper do WSL, precisará realizar a instalação setando a distribuição Linux desejada.
> ```ruby
>
> 1. Listagem das distribuições disponiveis:
>    $ wsl --list --online
> 2. Install WSL
>    $ wsl --install -d [distribuição desejada]
>      Ex: $ wsl --install -d Ubuntu
> ```

> **Updating WSL (in Windows terminal)**
> ```ruby
>
> $ wsl --update
> ```

> **Updating Ubuntu (in Linux terminal)**
> ```ruby
>
> $ sudo apt update

<br />

### ⛔ Errors

<br />

1) **Erro de DNS**
> 
> Caso apresente erro ao tentar realizar o update do **Linux**, provavelmente há configurado um proxy impedindo comunicações externas.
> Para resolver esse problema basta realizar a seguinte configuração:
> 1. **Editar ou criar o arquivo "/etc/wsl.conf" com o seguinte conteúdo:**
>    > ```ruby
>    > [network]
>    > generateResolvConf = false
>    > 
>    > [boot]
>    > command = "sudo printf 'nameserver 8.8.8.8\nnameserver 8.8.4.4' > /etc/resolv.conf"
>    > ``` 
>    > **Reiniciar o WSL:** (No Windows terminal)
>    > 
>    > ```ruby
>    > $ wsl --shutdown
>    > ```
>    > **Esperar 8s e reinicializar o WSL Ubuntu.**
>    > 
>    >    > Para reiniciar basta abrir um terminal do **WSL** novamente.
>
> 2. **Após esse procedimento o problema deverá ter sido resolvido. Volte a executar o command de atualização do "apt" no terminal do WSL Linux.**
>    > ```ruby
>    > $ sudo apt update
>    > ```

<br />

2) **Erro de inicialização do WSL**
>  
>  Caso apresente o seguinte erro no terminal ao tentar inicializar o WSL:
>    > ```ruby
>    > [process exited with code 4294967295 (0xffffffff)]
>    > ``` 
> Realizar o shutdown do WSL:
>    > ```ruby
>    > $ wsl --shutdown
>    > ``` 
> Realizar o restart da VM (PowerShell como administrador):
>    > ```ruby
>    > $ Get-Service LxssManager | Restart-Service
>    > $ Get-Service vmcompute | Restart-Service -force
>    > ``` 
> Após esse procedimento será possível inicializar o WSL novamente abrindo o terminal Linux

<br />


### 📌 Extras
> __Comandos básicos do ***WSL***__
> 
>   > **Versão atual**
>   > ```ruby
>   > $ wslfetch
>   > ```
> 
> __Documentação site microsoft ***WSL***__
> - [https://learn.microsoft.com/pt-br/windows/wsl/basic-commands](https://learn.microsoft.com/pt-br/windows/wsl/basic-commands)


<br />

## 📋 Notes

#### 1. wsl.conf
> Ao executar o __Linux__ pelo __WSL__, sempre que for reiniciado o sistema, os arquivos da pasta __ETC__ serão restaurados.
> Para poder persistir modificações de configurações padrão do sistema mesmo em sua reinicialização, Existe a possibilidade de configurar um arquivo especifico para essa finalidade, Esse arquivo se chama __`wsl.conf`__ que fica localizado dentro da pasta __ETC__ (se não existir deverá ser criado).
> No __`wsl.conf`__ é possivel configurar o stop de regeneração de certos arquivos e é possivel executar comandos logo após a todo boot realizado.
