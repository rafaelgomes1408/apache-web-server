# Servidor Web Simples com Apache

Este repositório contém a configuração e documentação para a instalação de um servidor web simples utilizando o Apache HTTP Server em uma instância EC2 da AWS.

## Índice

- [Introdução](#introdução)
- [Pré-requisitos](#pré-requisitos)
- [Configuração da Instância EC2](#configuração-da-instância-ec2)
- [Instalação do Apache](#instalação-do-apache)
- [Configuração do Servidor Web](#configuração-do-servidor-web)
- [Testando o Servidor](#testando-o-servidor)
- [Autores](#autores)
- [Licença](#licença)

## Introdução

Este projeto tem como objetivo configurar um servidor web básico utilizando o Apache. A configuração será feita em uma instância EC2 da AWS, dentro do nível gratuito, usando uma distribuição Linux.

## Pré-requisitos

Antes de começar, certifique-se de ter o seguinte:

- Conta na AWS com o nível gratuito ativado.
- Chave SSH para acesso à instância EC2.
- Conhecimentos básicos de Linux e SSH.

## Configuração da Instância EC2

1. Acesse o [AWS Management Console](https://aws.amazon.com/console/).
2. Navegue até o serviço EC2.
3. Clique em "Launch Instance".
4. Escolha a AMI (Amazon Linux 2 ou Ubuntu 20.04 LTS).
5. Selecione o tipo de instância `t2.micro` (elegível para o nível gratuito).
6. Configure as opções de instância conforme necessário.
7. Adicione armazenamento (8 GB padrão é suficiente).
8. Adicione tags para identificar a instância.
9. Configure o grupo de segurança para permitir acesso SSH (porta 22) e HTTP (porta 80).
10. Revise e lance a instância, criando ou usando uma chave SSH existente para acesso.

## Instalação do Apache

Conecte-se à instância EC2 via SSH:

```sh
ssh -i /path/to/key.pem ec2-user@<public-ip>  # Para Amazon Linux 2
```
```sh
ssh -i /path/to/key.pem ubuntu@<public-ip>  # Para Ubuntu
```

## Atualize os pacotes do sistema

```sh
sudo yum update -y  # Para Amazon Linux 2
```
```sh
sudo apt update && sudo apt upgrade -y  # Para Ubuntu
```

## Instale o Apache

```sh
sudo yum install httpd -y  # Para Amazon Linux 2
```
```sh
sudo apt install apache2 -y  # Para Ubuntu
```

## Configuração do Servidor Web

```sh
sudo systemctl start httpd  # Para Amazon Linux 2
```
```sh
sudo systemctl enable httpd  # Para Amazon Linux 2
```
```sh
sudo systemctl start apache2  # Para Ubuntu
```
```sh
sudo systemctl enable apache2  # Para Ubuntu
```

### Crie uma página web de exemplo

```sh
echo "<html><body><h1>Servidor Web Apache</h1><p>Este é um servidor web simples utilizando o Apache.</p></body></html>" | sudo tee /var/www/html/index.html
```

## Testando o Servidor

Abra seu navegador e acesse o endereço IP público da sua instância EC2. Você deve ver a página web de exemplo criada anteriormente.

```http://<public-ip>```

## Autores

Rafael Gomes

## Licença

Este README.md cobre todos os passos necessários para configurar e testar um servidor web simples com Apache em uma instância EC2 da AWS. Certifique-se de ajustar as partes específicas, como o seu nome e o link do seu perfil GitHub.
