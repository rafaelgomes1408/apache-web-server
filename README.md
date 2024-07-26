# Servidor Web Simples com Apache

Este repositório contém a configuração e documentação para a instalação de um servidor web simples utilizando o Apache HTTP Server em uma instância EC2 da AWS.

## Índice

- [Introdução](#introdução)
- [Pré-requisitos](#pré-requisitos)
- [Configuração da Instância EC2](#configuração-da-instância-ec2)
- [Instalação do Apache](#instalação-do-apache)
- [Configuração do Servidor Web](#configuração-do-servidor-web)
- [Permitir Tráfego HTTP (Porta 80)](#permitir-tráfego-http-porta-80)
- [Testando o Servidor](#testando-o-servidor)
- [Autores](#autores)
- [Licença](#licença)

## Introdução

Este projeto tem como objetivo configurar um servidor web básico utilizando o Apache. A configuração será feita em uma instância EC2 da AWS, dentro do nível gratuito, usando uma distribuição Debian.

## Pré-requisitos

Antes de começar, certifique-se de ter o seguinte:

- Conta na AWS com o nível gratuito ativado.
- Chave SSH para acesso à instância EC2.
- Conhecimentos básicos de Linux e SSH.

## Configuração da Instância EC2

1. Acesse o [AWS Management Console](https://aws.amazon.com/console/).
2. Navegue até o serviço EC2.
3. Clique em "Launch Instance".
4. Escolha a AMI (Debian).
5. Selecione o tipo de instância `t2.micro` (elegível para o nível gratuito).
6. Configure as opções de instância conforme necessário.
7. Adicione armazenamento (30 GB padrão é suficiente).
8. Adicione tags para identificar a instância.
9. Configure o grupo de segurança para permitir acesso SSH (porta 22) e HTTP (porta 80).
10. Revise e lance a instância, criando ou usando uma chave SSH existente para acesso.

## Instalação do Apache

Conecte-se à instância EC2 via SSH:

1. Baixe e instale o PuTTY.
2. Converta o arquivo '.ppk' fornecido o par de chaves durante a criação da instância EC2:
- Abrir o PuTTYgen
- Carregar a Chave:
   - Clique em "Load".
   - No diálogo de arquivo, selecione "All Files (*.*)" no campo de tipo de arquivo.
   - Navegue até o local onde está armazenado o seu arquivo `par_chaves.ppk` e selecione-o.
- Salvar a Chave Privada:
   - Clique em "Save private key".
   - Escolha um nome e local para salvar a chave privada no formato PuTTY (.ppk).
3. Configurar o PuTTY para Conexão
- Abrir o PuTTY
- Configurar o Hostname/IP:
   - No campo "Host Name (or IP address)", digite o endereço IP público da sua instância EC2.
- Configurar a Chave Privada:
   - No painel à esquerda, expanda "SSH" e clique em "Auth".
   - No campo "Private key file for authentication", clique em "Browse" e selecione o arquivo .ppk que você salvou anteriormente.
- Salvar a Sessão (Opcional):
   - Para facilitar o acesso futuro, você pode salvar essa configuração.
   - No painel à esquerda, clique em "Session".
   - No campo "Saved Sessions", digite um nome para a sessão e clique em "Save".
- Conectar:
   - Clique em "Open" para iniciar a conexão.
   - Na primeira vez que conectar, você verá um aviso de segurança. Clique em "Yes" para aceitar a chave do host e continuar.
4. Acessar a Instância:
- Quando solicitado, digite o nome de usuário para acessar a instância. Para instâncias Debian, o nome de usuário geralmente é `admin`, `root` ou `debian`. Verifique a documentação da AWS ou os detalhes da sua instância específica para confirmar o nome de usuário.

## Atualize os pacotes do sistema

```sh
sudo apt-get update && sudo apt-get upgrade -y  # Para Debian
```

## Instale o Apache

```sh
sudo apt-get install apache2 -y  # Para Debian
```

## Configuração do Servidor Web

```sh
sudo systemctl status apache2 # Para Debian
```
```sh
sudo systemctl start apache2  # Para Debian
```
```sh
sudo systemctl enable apache2  # Para Debian
```

## Permitir Tráfego HTTP (Porta 80)
Se durante a configuração da instância EC2, no passo 9. não foi configurada o tráfego HTTP, siga os passos abaixo:

1. Acesse o AWS Management Console.
2. Navegue até o serviço EC2.
3. Selecione sua instância e, na seção "Description" (Descrição), clique no ID do grupo de segurança associado à instância.
4. Na página do grupo de segurança, vá para a aba "Inbound rules" (Regras de entrada) e clique em "Edit inbound rules" (Editar regras de entrada).
5. Adicione uma nova regra com os seguintes detalhes:
   - Type: HTTP
   - Protocol: TCP
   - Port Range: 80
   - Source: 0.0.0.0/0 (para permitir o acesso de qualquer origem)
   - Description: Allow HTTP traffic
6. Clique em "Save rules" (Salvar regras) para aplicar as novas regras de entrada.

## Testando o Servidor

Abra seu navegador e acesse o endereço IP público da sua instância EC2. Você deve ver a página web padrão do apache localizada em /var/www/html/index.html 

```http://<public-ip>```

## Autores

Rafael Gomes

## Licença

Este README.md cobre todos os passos necessários para configurar e testar um servidor web simples com Apache em uma instância EC2 da AWS. Certifique-se de ajustar as partes específicas, como o seu nome e o link do seu perfil GitHub.
