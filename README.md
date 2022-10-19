*******
# Sumário
1. [Wordpress e MySQL com Docker-Compose](#1-wordpress-e-mysql-com-docker-compose)
    1. [Requisitos Mínimos para a instalação do Docker](#requisitos-mínimos-para-a-instalação-do-docker)
2. [Instalação do Docker no Windows, por Extenso](#2-instalação-do-docker-desktop-no-windows-por-extenso)
    1. [Como Abrir o Powershell em modo administrador](#1-para-a-instalação-do-docker-no-windows)
    2. [Como ativar o WSL](#2-digite-os-seguintes-comandos-no-powershell-para-ativar-o-wsl-windows-subsystem-for-linux)
    3. [Download e Instalação do Pacote de atualização de Kernel Linux](#4-faça-o-download-e-instalação-do-pacote-de-atualização-de-kernel-linux)
    4. [Comando para ativar o WSL2](#5-abra-novamente-o-powershell-em-modo-administrador-e-digite-o-comando)
    5. [Baixar e instalar o Docker](#6-por-fim-baixe-e-instale-o-docker-desktop-isso-pode-ser-feito-pelo-site-oficial-do-docker)
3. [Como mudar o login e senha do banco de dados (.env)](#3-como-mudar-o-login-e-senha-do-banco-de-dados-env)
    1. [Arquivo docker compose](#1-arquivo-docker-compose)
    2. [Arquivo .env](#2-arquivo-env)
5. [Como executar a Aplicação](#4-como-executar-a-aplicação)
    1. [Colocando os arquivos da aplicação em um diretório](#1-colocando-os-arquivos-de-docker-compose-e-env-no-diretório-desejado)
    2. [Copiando o caminho/diretório da aplicação](#2-copiar-o-caminho-do-diretório)
    3. [Abrindo o PowerShell e verificando o Docker](#3-abrindo-o-powershell-e-verificando-a-versão-do-docker)
    4. [Acessando o diretório do projeto no PowerShell](#4-mudando-para-o-diretório-do-projeto-no-powershell)
    5. [Subindo a Aplicação com 'docker compose up'](#5-subindo-a-aplicação-com-docker-compose-up)
    6. [Acessando a Aplicação em localhost:8080](#6-acessando-a-aplicação-em-localhost8080)
    7. [Wordpress Instalado com Sucesso!](#7-wordpress-e-mysql-funcionando-)
    
*******

# 1. Wordpress e MySQL com Docker-Compose:

Para a subirmos a aplicação do wordpress em conjunto com o MySQL via Docker-Compose, 
serão necessários os itens a seguir:
1. [Docker](https://www.docker.com)
2. [Docker-Compose](https://docs.docker.com/compose/install/)

> **Note**: A Instalação do Docker e Docker-Compose podem variar dependendo do sistema operacional utilizado, atenção para as instruções na documentação oficial do Docker!

## Requisitos Mínimos para a instalação do Docker:
  * 4GB Memória RAM
  * Processador 64-bit com suporte à Virtualização de hardware, a virtualização pode ser ativada nas configurações da BIOS. [Documentação sobre Virtualização](https://docs.docker.com/desktop/troubleshoot/topics/#virtualization) 

<details>
  <summary>Windows</summary>

  * Windows 10 64-bit: 
    * Versão 21H1 ou maior.
  * Windows 11 64-bit: 
    * Versão 21H2 ou maior.
  * Ativar o recurso WSL 2 no Windows. Para instruções detalhadas, siga a documentação da Microsoft: [Instalação WSL no Windows](https://docs.microsoft.com/en-us/windows/wsl/install-win10) 
  * Baixar e instalar o [Pacote de atualização de Kernel Linux](https://docs.microsoft.com/windows/wsl/wsl2-kernel)
  * Os Recursos de: Hyper-V e Containeres Windows devem estar ativados: [Instalação Hyper-V](https://learn.microsoft.com/pt-br/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)

</details>

<details>
  <summary>Linux</summary>

  * Suporte a virtualização KVM. Siga as instruções de [Virtualização KVM](https://docs.docker.com/desktop/install/linux-install/#kvm-virtualization-support) para verificar se os módulos do Kernel KVM estão ativados e como providenciar acesso ao dispositivo KVM.
  * QEMU deve estar na versão 5.2 ou mais novo. Recomenda-se atualizar para a ultima versão.
  * Sistema systemd init
  * Habilitar a configuração de Mapeamento de ID no namespaces de usuários, para maiores instruções, verifique a documentação de como habilitar o [Compartilhamento de Arquivo](https://docs.docker.com/desktop/faqs/linuxfaqs/#how-do-i-enable-file-sharing) 

</details>

---

# 2. Instalação do Docker Desktop no Windows, por Extenso:

### 1. Para a instalação do Docker no Windows:
Seguiremos as intruções da Documentação Oficial do Docker e da Microsoft: [Instalação Docker Desktop](https://docs.docker.com/desktop/install/windows-install/) [Instalação WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

Primeiro, devemos ativar o WSL (pode ser feito de formas diferentes), para isso, iniciaremos o PowerShell em modo Administrador.

Na aba de pesquisa do Windows, digite "powershell", e execute-o em modo administrador, como demonstrado a seguir:

<details>
 <summary><strong>Imagens: Como Abrir o PowerShell em modo Administrador</strong></summary>
 
![Procurar Powershell](https://user-images.githubusercontent.com/65841249/196262334-84674994-d036-4f37-a47a-f0d2427da686.png)
 
![Executar Powershell em modo ADM](https://user-images.githubusercontent.com/65841249/196262376-8e2a23e9-f4eb-4129-b6a0-7cd182a1a6a4.png)
 
</details>

---

### 2. Digite os Seguintes comandos no powershell para Ativar o WSL (Windows SubSystem for Linux): 

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

<details>
 <summary><strong>Imagens: Comandos no Powershell</strong></summary>
 
 ![Comando 1](https://user-images.githubusercontent.com/65841249/196264815-c207472b-120f-41f4-a4a5-f2292e9d89c6.png)
 
 ![Comando 2](https://user-images.githubusercontent.com/65841249/196264943-c8bd881b-463a-4e32-b8be-3784c41d5049.png)

</details>

---

### 3. Reinicie o Computador

---

### 4. Faça o Download e instalação do Pacote de atualização de Kernel Linux:
Pode ser encontrado no site oficial em: [Instalação WSL2](https://docs.microsoft.com/windows/wsl/wsl2-kernel)
(Também pode ser baixado diretamente em: [WSL2 Download MSI](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi))

---

### 5. Abra novamente o powershell em modo Administrador e Digite o comando:
```powershell
wsl --set-default-version 2
```
Assim, definindo o WSL2 como padrão ao invés do WSL.

![Set WSL2 no PowerShell](https://user-images.githubusercontent.com/65841249/196265405-b12f186f-b314-44e8-964d-911eabf78df7.png)

---

### 6. Por fim, Baixe e instale o Docker Desktop, isso pode ser feito pelo [Site Oficial do Docker](https://www.docker.com/).
![Docker Desktop Windows Download](https://user-images.githubusercontent.com/65841249/196259705-d0fc1351-523b-4bcd-a0d7-efafc1b91958.png)

---

### 7. Reinicie o Computador, e pronto!

![Docker Desktop Instalado e funcionando](https://user-images.githubusercontent.com/65841249/196265723-bc870492-4442-4b83-92a4-5439f3116de0.png)

---

# 3. Como mudar o login e senha do banco de dados (.env)

## Para a aplicação funcionar de maneira correta, teremos dois arquivos:

### 1. Arquivo docker-compose:
```yaml
version: '3.9'

services:
  mysql_service:
    image: "mysql:${MYSQL_VERSION}"
    restart: always
    ports:
      - 3306:3306
    environment:
      MYSQL_DATABASE: "${DATABASE_NAME}"
      MYSQL_USER: "${WORDPRESS_DB_USER}"
      MYSQL_PASSWORD: "${WORDPRESS_DB_PASSWORD}"
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - .\mysql_vol:/var/lib/mysql
    networks:
      - wp_network

  wordpress_service:
    image: "wordpress:${WORDPRESS_VERSION}"
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: mysql_service
      WORDPRESS_DB_NAME: "${DATABASE_NAME}"
      WORDPRESS_DB_USER: "${WORDPRESS_DB_USER}"
      WORDPRESS_DB_PASSWORD: "${WORDPRESS_DB_PASSWORD}"
    volumes:
      - .\wp_vol:/var/www/html
    networks:
      - wp_network
    depends_on:
      - mysql_service

networks:
  wp_network:
    driver: bridge

volumes:
  wp_vol:
  mysql_vol:
```
  
### 2. Arquivo .env:

--- 
* Arquivo responsavel por ditar as versões das aplicações.
  * MYSQL_VERSION=<versão_imagem_mysql>
  * WORDPRESS_VERSION=<versão_imagem_wordpress>
* O nome do banco de dados mysql.
  * DATABASE_NAME=<nome_do_banco_de_dados>
* O usuario e a senha do banco de dados.
  * WORDPRESS_DB_USER=<usuario_banco_de_dados>
  * WORDPRESS_DB_PASSWORD=<senha_banco_de_dados>

```
MYSQL_VERSION=8.0.31
WORDPRESS_VERSION=6.0.2

DATABASE_NAME=wordpressdb

WORDPRESS_DB_USER=usuariodb
WORDPRESS_DB_PASSWORD=senhaforte123
```

### 3. Como mudar o usuário e senha do banco de dados
Para mudar o usuário e senha do banco de dados, deve mudar as variáveis:
`WORDPRESS_DB_USER` e `WORDPRESS_DB_PASSWORD` no arquivo .env, 
Pois são referentes ao usuário e senha do banco de dados respectivamente.

# 4. Como executar a Aplicação

### 1. Colocando os arquivos de docker-compose e .env no diretório desejado.

Crie uma pasta e coloque os arquivos de docker-compose e .env em um diretório de sua preferência.
> Obs: Acima dos arquivos é possivel observar o caminho/diretório de pastas.

![Pasta windows caminho diretorio](https://user-images.githubusercontent.com/65841249/196267055-69de3122-fa87-4e5d-bcd2-6dd978e83026.png)

---

### 2. Copiar o caminho do diretório

Copie o caminho de onde está o docker-compose e .env, como demostrado na imagem. 
> Obs: o caminho poderá mudar de acordo com cada maquina e local que os arquivos estão salvos.

![Pasta windows copiar caminho](https://user-images.githubusercontent.com/65841249/196267074-b9a143bb-f10b-4242-bfb9-f742a02d7584.png)

---
### 3. Abrindo o Powershell e verificando a versão do Docker
Abra o powershell e aplique o comando `docker --version` no powershell para visualizar a versão do docker e se o mesmo está sendo executado de maneira correta em sua maquina.

![DockerVersion no powershell](https://user-images.githubusercontent.com/65841249/196267125-caf20b4f-64f8-47fe-98bc-6f4eb6737e23.png)

---
### 4. Mudando para o diretório do projeto no powershell
Aplique o comando `cd <diretório_do_arquivo_docker_compose>` para se direcionar para o diretório onde os arquivos estão localizados. 
 
![cd diretorio compose powershell](https://user-images.githubusercontent.com/65841249/196267154-bd718cfc-0574-44fb-b827-a3f1b7bfc6a1.png)

---
### 5. Subindo a aplicação com 'docker compose up'
Utilize o comando `docker compose up` para subir a aplicação 

![docker compose up powershell](https://user-images.githubusercontent.com/65841249/196267186-287f9b59-1425-4664-b642-1653e577db79.png)

---
### 6. Acessando a Aplicação em 'localhost:8080'
Com isso, a aplicação deverá estar disponível em `localhost:8080` e a tela de instalação do wordpress ira aparecer com a opção de escolher a linguagem.
> Obs: Pode demorar alguns minutos até o Docker-Compose subir o Wordpress e o Banco de dados.

<details>
  <summary>Imagem: Docker-Compose subindo as aplicações</summary>
  
  ![docker compose executando...](https://user-images.githubusercontent.com/65841249/196267345-00a6f5c2-524f-4b1c-b29d-907ae5ba716a.png)
  
</details>

---
### 7. Wordpress e MySQL funcionando !
Por fim, digite as informações solicitadas e aperte o botão "Instalar Wordpress". 
E com isso, o Wordpress estará instalado e operando com sucesso!

<details>
  <summary>Imagens: Aplicação Wordpress funcionando</summary>
  
  ![Wordpress Funcionando 1](https://user-images.githubusercontent.com/65841249/196563327-fab5aecb-5d30-4e9d-a240-775ecf25b2d8.png)

  ![Wordpress Funcionando 2](https://user-images.githubusercontent.com/65841249/196563332-11933b0a-dd4a-4295-9ac6-2001054476dd.png)

  ![Wordpress Funcionando 3](https://user-images.githubusercontent.com/65841249/196563334-2179a6c8-45b5-474d-ac2f-785d5d85674d.png)

</details>

---
