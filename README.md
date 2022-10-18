# Atividade_DevSecOps_Docker realizada durante o estágio na Compass - DevSecOps #

- Esse repositório tem como objetivo mostrar como subir uma aplicação Wordpress + DB Mysql utilizando docker.
- Desenvolvido por: Lucas Martins Ribeiro e João Fellipe Lemos Costa

# Instalação do Docker Desktop no Windows #
  - Utilize a documentação disponibilizada no site do Docker: https://docs.docker.com/desktop/install/windows-install/

# Instalação Docker Engine e Docker Compose para Ubuntu Usando Repositório #

1. Desinstale versões mais antigas do Docker

	$ sudo apt-get remove docker docker-engine docker.io containerd runc

2. Atualize os pacotes do computador

	$ sudo apt-get update

3. Instale os pacotes para permitir o acesso ao repositório HTTPS

	$  sudo apt-get install \
		 ca-certificates \
		 curl \
		 gnupg \
		 lsb-release

4. Adicione a chave GPG oficial do Docker

	$ sudo mkdir -p /etc/apt/keyrings
	$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

5. Configura o repositório

	$ echo \
	"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
	$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

6. Atualize os pacotes novamente
	
	$ sudo apt-get update
	Em caso de erro na atualização dos pacotes tente definir o umask do computador com o comando:

	$ sudo chmod a+r /etc/apt/keyrings/docker.gpg

7. Instale a versão mais recente do Docker Engine e Docker Compose 

	$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Criação do Wordrpess Vinculado ao Banco de Dados MySql #


1. Para iniciar  é criar uma arquivo com a extensão “.yml”, para isso usamos o comando:
	touch arquivo-docker.yml

2. Após criar o arquivo “arquivo-docker.yml”, precisamos configurá-lo com a linguagem YML. Vamos usar a seguinte configuração para baixar as imagens mysql e wordpress com as seguintes configurações de variáveis de ambiente. Para fazer a edição usamos o comando:

	vim arquivo-docker.yml

E inserimos a seguinte programação e salvamos o documento.

	version: '3.4'

	services:
	  db:
	    image: mysql:latest
	    command: mysqld --default_authentication_plugin=mysql_native_password
	    restart: always
	    environment:
	      TZ: America/Sao_Paulo
	      MYSQL_ROOT_PASSWORD: docker
	      MYSQL_USER: docker
	      MYSQL_PASSWORD: docker
	      MYSQL_DATABASE: wordpress
	    ports:
	      - "3308:3306"
	    networks:
	      - wordpress-network
	  wordpress:
	    image: wordpress:latest
	    ports:
	      - 80:80
	    volumes:
	      - ./config/php.conf.uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
	      - ./wp-app:/var/www/html
	    restart: always
	    environment:
	      TZ: America/Sao_Paulo
	      WORDPRESS_DB_HOST: db
	      WORDPRESS_DB_NAME: wordpress
	      WORDPRESS_DB_USER: root
	      WORDPRESS_DB_PASSWORD: docker
	    depends_on:
	      - db
	    networks:
	      - wordpress-network
	networks:
	    wordpress-network:
	      driver: bridge

3. Depois do arquivo YML configurado, no mesmo diretório que está localizado o arquivo executamo o arquivo com o comando:

	docker-compose up
	
Após a execução desse comando iniciará o processo de instalação de imagens, configuração das variáveis de ambiente e criação dos contêineres.

5. Com o processo de instalação terminado basta verificar se está tudo funcionando, para isso vá no navegador e digite “localhost:80” e  aperta enter. Se tudo estiver certo aparecerá a página de configuração do wordpress.
	

