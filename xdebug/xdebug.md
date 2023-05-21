# Xdebug <span align="right">- Instalação e documentação de comandos.</span>

![This is an image](/images/xdebug.png)
[:back:](/README.md) [home](/README.md) | **Xdebug**

<br>


## 📋 Notes (Ubuntu in WSL2)

#### 1. Requesitos
> Necessário a instalação do modulo fpm do PHP.
> > Exemplo (Caso tenha esquecido de instalar o módulo na instalação do PHP):
> > > ```ruby
> > > $ sudo apt install php8.2-fpm
> > > ```
> Configuração do arquivo 

#### 2. Configuração do xdebug.ini
> Instalação do xdebug:
> > ```ruby
> > $ sudo apt install php-xdebug
> > ```
> Configuração do arquivo mods-available/xdebug.ini:
> > ```ruby
> > zend_extension=xdebug.so
> > xdebug.mode=debug
> > ```

#### 3. Configuração do xdebug.ini Com Docker (Laravel Sail)
> Em ambiente docker, como por exemplo Laravel Sail, é preciso realizar alguns passos extras, para que seja possível o xdebuger acessar um container no docker será necessário adicionar mais os seguintes códigos:
> Parametros a mais no mods-available/xdebug.ini:
> > ```ruby
> > xdebug.discover_client_host=0
> > xdebug.client_host=host.docker.internal
> > ```
> > 
> > Criar um link do xdebug.ini para "/etc/php/8.2/cli/conf.d/", caso apresente a mensagem que já exista, apenas verifique se no arquivo 20-xdebug.ini está igual ao xdebug.ini.
> > ```ruby
> > $ sudo ln -s /etc/php/8.2/mods-available/xdebug.ini /etc/php/8.2/cli/conf.d/20-xdebug.ini
> > ```

#### 4. VSCode, criação do arquivo .vscode/launch.json
> Para a configuração no docker é preciso realizar alguns passos extras, para que seja possível o xdebuger acessar um container no docker será necessário adicionar mais os seguintes códigos:
> Parametros a mais no mods-available/xdebug.ini:
> > ```ruby
> > xdebug.discover_client_host=0
> > xdebug.client_host=host.docker.internal
> > ```

<br />

### 🚀 Links
> ```ruby
> $ some code...
> ```


