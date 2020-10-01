# dockerTR
CCO - Laravel 

Projeto desenvolvido pelo UNIFEG no curso de CCO - Oitavo Período

# definindo a imagem base do sistema operacional.
FROM ubuntu:20.04
LABEL maintainer ="Falconi"
# Atualiza todas bibliotecas 

RUN apt-get update && DEBIAN_FRONTEND="noninteractive" apt-get -y install tzdata apt-utils
RUN apt-get install -y build-essential php7.4 php7.4-dev \\
php7.4-cgi php7.4-cli php7.4-common php7.4-bcmath php7.4-fpm php7.4-xml phpdox php7.4-mbstring php7.4-json \\
php7.4-zip php7.4-pgsql php7.4-mbstring unzip composer && mkdir -p /home/app
WORKDIR /home/app
RUN composer global require laravel/installer && composer -vvv create-project --prefer-dist laravel/laravel blog
#O RUN executa comandos DENTRO do container. 
RUN apt-get -y install nano vim
RUN apt-get install nginx -y
WORKDIR /home/app/blog
ENTRYPOINT ["php","artisan","serve","--host","0.0.0.0"]
RUN apt-get install nginx -y
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]



REPOSITORY          TAG                 IMAGE ID
ubuntu              20.04               c045485c74c1
