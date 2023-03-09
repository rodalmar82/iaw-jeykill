---
layout: post
title:  "Practica"
date:   2023-03-09 13:15:34 -0600
categories: jekyll update
---
# iaw-practica02
## Instalación de LAMP sack en RHEL por Rodrigo Alarcón Márquez


## 1º Paso: Creación de Estancia en Amazon

Dentro de AWS Academy creamos una nueva estancia.

Le tendremos que asignar un nombre, en aplicaciones escogeremos Red Hat y en el tipo de instancia tendremos que escoger una que posea al menos 2 GB de memoria.  

La llave que escogeremos será Vodkey y abriremos los puertos SSH, HTTPS y HTTP.



![Error]({{ site.url }}/images/practica3/Captura1RH.png){: .center}{:width="200px"}

![Error]({{ site.url }}/images/practica3/Captura2RH.png){: .center}{:width="200px"}
## 2º Paso: IP Elastica

A la estancia que acabamos de crear deberemos de asignarle una IP elastica.

![Error]({{ site.url }}/images/practica3/Captura3RH.png){: .center}{:width="200px"}

## 3º Paso: Virtual Box

Abrimos Virtual Box y dentro del explorador remoto agregamos la nueva estancia con la clave que podemos encontrar conectando con la instancia en la sección SSH client.

![Error]({{ site.url }}/images/practica3/Captura4RH.png){: .center}{:width="500px"}

## 4º Paso: Conexión con cliente SSH

Dentro de Virtual Box conectamos con el cliente SSH haciendo click en la esquina verde inferior izquierda. Deberemos marcar que queremos trabajar con Linux y poner la dirección del cliente.

![Error]({{ site.url }}/images/practica3/Captura5RH.png){: .center}{:width="400px"}


## 5º Paso: Actualización y conexión con Github

Una vez hemos accedido, ya podemos trabajar con el terminal.

Comenzaremos actualizando todos los repositorios con el comando:
```bash
 sudo apt-get update.
```

A continuación utilizaremos deberemos de instalar la extensión de git con el comando:  
```bash
 sudo apt-get install git
 ```

Tras ello, asignaremos un nombre y correo electronico con los comandos:  
```bash
**git config --global user.name "Nombre"**

 **git config --global user.email "correo@electronico .com"**
```
Podrémos comprobar el cambio con el comando: 
```bash
 **git config --list**
```
Por último enlazaremos virtual Box con un clon de nuestro repositorio de Git hub con el comando:  

**git clone https:// github.com/Nombre_de_Repositorio/taller-git-github.git**

Tras hacerlo, una carpeta con el nombre del repositorio debería de haber aparecido en el árbol de la izquierda.


## 6º Paso: Creación de las carpetas

Dentro del directorio recien creado (iaw-practica02 en mi caso), creamos las carpetas **php** y **script**.  

Dentro de php crearemos un archivo llamado **info.php** y dentro de script crearemos otro archivo llamado **lamp_tools-sh.**

Será dentro de lamp_tools.sh donde escribiremos los comandos que automatizarán las instalaciones.


![Error]({{ site.url }}/images/practica3/Captura6RH.png){: .center}{:width="300px"}

## 7º Paso: Creación del script

Comenzamos el scrip con:
```bash
**#!/bin/bash**  
**set -x**
```

Actualizamos los repositorios con el comando: 
```bash 
sudo dnf update
```

Instalamos el servidor web apache
```bash
dnf install httpd -y
```
Iniciamos el servidor web apache
```bash
systemctl start httpd
```
Habilitamos el servidor web apache
```bash
systemctl enable httpd
```
Abrir puertos en caso de tener activo Firewall
```bash
Firewall-cmd --zone=public --add-service=http
Firewall-cmd --zone=public --add-service=https
```

Instalamos el servidor de MySQL
```bash
dnf install mysql-server -y
```

Iniciamos el servidor MySQL
```bash
systemctl start mysqld
```
Habilitamos el servidor MySQL
```bash
systemctl enable mysqld
```
Instalamos los módulos de PHP
```bash
dnf install php -y
```
Instalamos las extensiones de PHP
```bash
dnf install php-mysqlnd -y

dnf install php-zip php-json php-fpm -y
```
Habilitamos el servidor de FPM
```bash
systemctl enable --now php-fpm
```
Reiniciamos Apache despues de la instalación
```bash
systemctl restart httpd
```
Copiamos el archivo para ver que se ha instalado.
```bash
cp ../php/info.php /var/www/html
```
Instalamos los repositorios necesarios para phpMyAdmin
```bash
dnf install -y wget php-pdo php-pecl-zip php-common php-mbstring php-cli php-xml tar
dnf install -y php-mbstring 
```
Instalación de phpMyAdmin
```bash
wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.
```
Descomprimimos el paquete
```bash
tar -zxvf phpMyAdmin-latest-all-languages.tar.gz
```
Instalamos Adminer  

Para ello creamos un directorio para Adminer
```bash
mkdir /var/www/html/adminer
```
Descargamos el archivo de Adminer
```bash
wget https://github.com/vrana/adminer/releases/download/v4.8.1/adminer-4.8.1-mysql.php
```

Por ultimo daremos permisos al script con 
```bash
chmod a+x lamp_tools.sh
```

![Error]({{ site.url }}/images/practica3/Captura7RH.png){: .center}{:width="400px"}

![Error]({{ site.url }}/images/practica3/Captura8RH.png){: .center}{:width="500px"}

## Paso final: Ejecutamos el script

Para ejecutarlo deberemos de  ejecutar dentro del directorio iaw-practica02 en el terminal el comando: 
```bash
sudo ./lamp_tools.sh
```

  
![Error]({{ site.url }}/images/practica3/Captura9RH.png){: .center}{:width="400px"}

![Error]({{ site.url }}/images/practica3/Captura10RH.png){: .center}{:width="400px"}
