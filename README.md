# Atividade_DevSecOps_Docker realizada durante o estágio na Compass - DevSecOps #

- Esse repositório tem como objetivo mostrar como subir uma aplicação Wordpress + DB Mysql utilizando docker.
- Desenvolvido por: Lucas Martins Ribeiro e João Fellipe Lemos Costa

# Instalação do Docker Desktop no Windows #
  - Utilize a documentação disponibilizada no site do Docker: https://docs.docker.com/desktop/install/windows-install/

# Instalação do Docker no Linux usando um script #
  - sudo apt-get update
  - curl -fsSL https://get.docker.com -o get-docker.sh
  - sudo sh get-docker.sh
  
  - Depois você pode rodar o comando "sudo service docker status" para verificar se o docker está rodando.

# Rodar o projeto utilizando docker-compose #
 - git clone https://github.com/lucasmartinsribeiro/Atividade_DevSecOps_Docke.git
 - cd docker-compose/
 - docker-compose up
