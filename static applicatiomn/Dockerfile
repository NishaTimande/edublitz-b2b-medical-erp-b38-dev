FROM ubuntu:latest
#base image is added

LABEL dev="Nisha"
#giving tag to the docker

RUN apt-get update && \
    apt-get install apache2 unzip -y && \
    rm -rf /var/www/html/index.html 
#we install webserver ,unzip package & update the same image

ADD https://templatemo.com/download/templatemo_623_novapay  /var/www/html/templatemo_623_novapay
#we download the static page from internet & move it ibn /var/www/html/templatemo_623_novapay

WORKDIR /var/www/html
#changing/switching directories to /var/www/html

RUN unzip templatemo_623_novapay.zip && \
    mv templatemo_623_novapay/*  /var/www/html/

#unzip the directory & move staic code into /var/www/html
 
EXPOSE 80
# container will be having open 80 port

CMD  ["apachectl", "-D", "FOREGROUND"]
