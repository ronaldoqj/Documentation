# WSL <span align="right">- Instalação e documentação de comandos.</span>

![This is an image](/images/wsl-header.jpg)
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
> 


> **Obs:** Caso apresente erro ao tentar realizar o update do **Linux**, provavelmente há configurado um proxy impedindo comunicações externas.
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

### 📌 Extras
> __Comandos básicos do ***WSL***__
> - [https://learn.microsoft.com/pt-br/windows/wsl/basic-commands](https://learn.microsoft.com/pt-br/windows/wsl/basic-commands)
