---
layout: post
title: Instalando y configurando un servidor Apache
subtitle: Desde tu localhost
cover-img: /assets/img/apache-server.jpg
# thumbnail-img: /assets/img/thumb.png
# share-img: /assets/img/path.jpg
tags: [backend]
---

{: .box-note}
En este tutorial te guiaré paso a paso para que crees tu propio servidor local utilizando Apache. Adicionalmente, aprenderemos a traer los datos de nuestro repositorio en github hasta el servidor y visualizarlos en la web.

## Antes de ello, comprendamos ¿qué es un servidor web?
 
Un servidor web es un programa que te permite mostrar los archivos que contienen las páginas web a los usuarios, en respuesta a sus solicitudes, las cuales son enviadas a través de internet. Sin embargo, hay computadoras y dispositivos dedicados que también pueden llamarse servidores web.

En este tutorial vamos a ver cómo usar Apache para tener nuestro servidor usando nuestro propio computador.

## Pero, ¿Qué es Apache?
Apache es un software de servidor web gratuito y de código abierto creado para plataformas unix (Linux, Mac), el cual nos permite servir o mostrar las páginas de nuestro sitio.

Ahora que ya sabemos esto, ¡comencemos!

## Paso 1 – Instalando el servidor
Como te mencioné anteriormente, Apache está enfocado para plataformas unix, para este tutorial vamos a utilizar una máquina en Linux Ubuntu 20.04 LTS.
 

Apache se encuentra disponible dentro de los repositorios de software predeterminados de Ubuntu, esto nos facilita la instalación por medio de herramientas convencionales para administración de paquetes.

Lo primero que haremos es actualizar nuestro índice de paquetes locales. Esto nos garantizará que en él se encuentren las versiones mas recientes de los paquetes.
 

Siéntete libre de abrir la terminal de línea de comandos, en ubuntu puedes usar CTRL + ALT + T para abrirla.

```bash
sudo apt update
Ahora, instalemos el paquete apache2:

sudo apt install apache2
```

Luego de confirmar la instalación, apt instalará Apache al igual que todas las dependencias adicionales que requiera.

## Paso 2 – Configurar el cortafuegos (Firewall)
Antes de comenzar a usar Apache, debemos modificar unas reglas del cortafuegos, de modo que se permita el acceso externo por defecto. Por defecto el cortafuegos está configurado con una restricción de acceso al servidor.

Durante la instalación, Apache se registra en el UFW para proveer los perfiles que permitan habilitar o deshabilitar su acceso a través del cortafuego.

Puedes listar los perfiles de ufw digitando:
```bash
sudo ufw app list
```
Esto te debe salir en consola:
```bash
Aplicaciones disponibles:
  Apache
  Apache Full
  Apache Secure
```
Como hemos visto, existen tres perfiles disponibles para Apache, hablemos un poco de ellos:

Apache: este perfil habilita únicamente el puerto 80 (normal, tráfico web sin encriptar).
Apache Full: este perfil habilita dos puertos: puerto 80 (normal, tráfico web sin encriptar) y el puerto 443 (tráfico encriptado mediante TLS/SSL).
Apache Secure: este perfil habilita únicamente el puerto 443 (tráfico encriptado mediante TLS/SSL).
Es recomendable habilitar el perfil de mayor restricción en ambientes productivos. Como aún no tenemos SSL configurado y estamos en un ambiente de pruebas, permitiremos el tráfico a través del puerto 80 de la siguiente forma:
```bash
sudo ufw allow 'Apache'
```
Podemos verificar el cambio escribiendo:
```bash
sudo ufw status
```
Debes recibir esta respuesta:
```bash
Estado: activo

Hasta                      Acción      Desde
-----                      ------      -----
Apache                     ALLOW       Anywhere                  
Apache (v6)                ALLOW       Anywhere (v6)
```   
Como puedes observar, el perfil ha sido activado, y el acceso al servidor web es permitido.

Apache se inicia por defecto cuando termina la instalación, si quieres verificarlo, abre tu navegador y en el campo de direcciones puedes escribir localhost + ENTER.

Si quieres aprender más acerca de todo lo que puedes hacer con tu servidor de apache, ingresa al Curso de Administración de Servidores Linux.

## Paso 3 – Clona tu sitio desde Github a tu servidor
Para realizar este paso, debemos saber que Apache toma los archivos del servidor desde la carpeta /var/www/html por defecto, así que allí es donde colocaremos nuesto sitio.

Desde la terminal, nos movemos a la carpeta /var/www/html:
```bash
cd /var/www/html
```
Clonamos nuestro repositorio con git clone <url_repo>.

En este ejemplo usaré un repositorio que ya tengo creado, si deseas puedes clonarlo o hacer fork al mismo para crear tu propia versión.

En esta carpeta es necesario un permiso de administrador para hacer algunas cosas, así que no olvides iniciar el comando con la palabra sudo.
```bash
sudo git clone https://github.com/cristian-rincon/css-google-clone.git
```
Si todo ha salido bien, te saldrá esto en consola:
```
Clonando en 'css-google-clone'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 9 (delta 1), reused 5 (delta 0), pack-reused 0
Desempaquetando objetos: 100% (9/9), 3.18 KiB | 651.00 KiB/s, listo.
```
Ahora volvamos a nuestro navegador y escribamos localhost/css-google-clone/ + ENTER.

Esto leerá el archivo index.html que se encuentra en el proyecto. Si usaste el repositorio que empleamos en este ejemplo, vas a ver un clon(visual) de Google.
Google Clone

A partir de aquí, puedes continuar con la creación de tu sitio web teniendo tu propio servidor local y realizar el versionamiento de tu proyecto con git y Github.