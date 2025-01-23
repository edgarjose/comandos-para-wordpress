# comandos-para-wordpress
Instalação do WordPress numa instância EC2.


## Passo 1: Atualizar pacotes do sistema
sudo yum update -y

## Passo 2: Instalar o Apache (HTTPD)
sudo yum install httpd -y

## Passo 3: Iniciar o Apache e configurá-lo para iniciar automaticamente na inicialização

sudo systemctl start httpd

sudo systemctl enable httpd

## Passo 4: Instalar PHP 7.4
sudo amazon-linux-extras install -y php7.4

sudo systemctl restart httpd

## Passo 5: Instalar MariaDB
sudo yum install -y mariadb-server

## Passo 6: Iniciar o MariaDB e configurá-lo para iniciar automaticamente na inicialização
sudo systemctl enable mariadb

sudo systemctl start mariadb

## Passo 7: Configurar a segurança do MariaDB
sudo mysql_secure_installation

## Passo 8: Aceder ao MariaDB
mysql -u root -p

## Passo 9: Criar a base de dados para o WordPress
CREATE DATABASE wordpressdb;

## Passo 10: Criar um utilizador para a base de dados
CREATE USER 'dbuser'@'localhost' IDENTIFIED BY 'admin123';

## Passo 11: Conceder permissões ao utilizador para aceder à base de dados

GRANT ALL PRIVILEGES ON wordpressdb.* TO 'dbuser'@'localhost';

## Passo 12: Atualizar as permissões
FLUSH PRIVILEGES;

## Passo 13: Baixar e extrair o WordPress
cd /tmp

sudo wget https://wordpress.org/latest.tar.gz

sudo tar xzvf latest.tar.gz


## Passo 14: Configurar o WordPress
cd wordpress

sudo mv wp-config-sample.php wp-config.php

sudo vi wp-config.php

define('DB_NAME', 'wordpressdb');

define('DB_USER', 'dbuser');

define('DB_PASSWORD', 'admin123');

define('DB_HOST', 'localhost');

## Passo 15: Mover os ficheiros do WordPress para o diretório do Apache
sudo mv wordpress/* /var/www/html/

## Passo 16: Definir permissões adequadas para o Apache
sudo chown -R apache:apache /var/www/html/

## Passo 17: Reiniciar o Apache
sudo systemctl restart httpd

