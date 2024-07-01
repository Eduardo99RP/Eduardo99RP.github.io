---
layout: single
title: Maquina Headless
excerpt: "Abordando el desafío de la máquina Headless en HackTheBox: una intrigante aventura que, aunque aparentemente sencilla, esconde múltiples desafíos y lecciones clave."
date: 2024-06-30
classes: wide
header:
  teaser: /assets/images/MaquinaHeadless/headless.png
  teaser_home_page: true
categories:
  - HackTheBox
tags:
  - puerto 5000
  - nmap
---


<p align="center">
<img src="/assets/images/MaquinaHeadless/Aspose.Words.c51fa9d9-6a10-477b-b35c-8f7240e81596.001.png">
</p>


# **Maquina Headless**

En esta máquina primero que nada se tuvo que hacer un análisis para poder obtener información sobre los puertos que estaba abierto para ello se llevó a cabo el uso NMAP, en el cual se hace con el siguiente comando:

```sh
nmap -p- -sC -vvv –min-rate 5000 -n 10.10.11.8 
```


- **-p-**: Este parámetro indica que Nmap debe escanear todos los puertos, del 1 al 65535. Normalmente, Nmap escanea solo los 1000 puertos más comunes si no se especifica ningún rango de puertos.

 

- **-sC**: Este parámetro habilita el uso de los scripts Nmap Scripting Engine (NSE) con la opción de script predeterminado. Los scripts NSE pueden realizar una variedad de tareas, como la detección de versiones de servicios y la identificación de vulnerabilidades.

 

- **-vvv**: Este parámetro aumenta la verbosidad del escaneo, proporcionando información detallada sobre el progreso del escaneo y los resultados. Cuantos más "v" se añadan, más detallada será la salida.

 

- **–-min-rate 5000**: Este parámetro establece la tasa mínima de paquetes por segundo que Nmap debería enviar, en este caso, 5000 paquetes por segundo. Esto hace que el escaneo sea más rápido, pero puede generar tráfico de red considerable y posiblemente ser detectado como un comportamiento sospechoso por sistemas de detección de intrusos (IDS).

 

- **-n**: Este parámetro deshabilita la resolución de nombres de dominio inversa. Esto significa que Nmap no intentará resolver direcciones IP a nombres de host, lo que puede acelerar el escaneo.

**Resultados obtenidos:**

<p align="center">
<img src="/assets/images/MaquinaHeadless/Aspose.Words.c51fa9d9-6a10-477b-b35c-8f7240e81596.002.png">
</p>

En la captura podemos ver que solo tenemos abiertos dos puertos el cual uno es el puerto 22 y el otro el 5000, cual sabemos las siguientes características:



**Puerto 22**

- **Protocolo:** TCP
- **Servicio común:** SSH (Secure Shell)
- <a name="_int_ahikk2d5"></a>**Uso principal:** El puerto 22 es conocido por el protocolo SSH, que proporciona una forma segura de conectarse a otro ordenador a través de una red no segura. SSH permite el acceso remoto a servidores, la transferencia segura de archivos mediante SCP (Secure Copy) y SFTP (SSH File Transfer Protocol), así como la ejecución remota de comandos. SSH es esencial en la administración de sistemas y servidores, especialmente en entornos Linux y Unix.

**Puerto 5000**

- **Protocolo:** TCP/UDP
- **Servicios comunes:**
  - **UPnP (Universal Plug and Play):** Este protocolo, utilizado principalmente en redes domésticas, permite que dispositivos en una red se descubran y se comuniquen automáticamente entre sí. UPnP facilita la configuración de redes y la conectividad entre dispositivos sin intervención manual significativa.
  - **Docker:** En el contexto de Docker, un sistema de contenedores de aplicaciones, el puerto 5000 se usa comúnmente como el puerto predeterminado para el registro privado de Docker (Docker Registry). Un Docker Registry es un repositorio para almacenar y distribuir imágenes Docker.
  - **Flask:** En el desarrollo web con Python, el marco Flask puede usar el puerto 5000 como su puerto predeterminado para ejecutar aplicaciones web durante el desarrollo.
- **Uso principal:** Dado que el puerto 5000 no está asignado de manera oficial a un servicio específico por la IANA (Internet Assigned Numbers Authority), puede ser utilizado por diferentes aplicaciones y servicios según las necesidades de los usuarios y desarrolladores. Sin embargo, los usos mencionados arriba son algunos de los más comunes.

A continuación, procedemos a obtener más información de los puertos usando nmap esto se hace principalmente para que no se demore demasiado tiempo en obtener la información:

```sh
nmap -p22,5000 -A -Pn -vvv 10.10.11.8
```


- **-p22,5000**: Esta opción especifica los puertos que deseas escanear. En este caso, Nmap escaneará los puertos 22 (usualmente usado por SSH) y 5000. Puedes especificar un rango de puertos o una lista separada por comas.
- **-A**: Esta opción activa la detección avanzada. Incluirá:
  1. Detección de sistema operativo.
  1. Detección de versión de servicio.
  1. Escaneo de scripts.
  1. Rastreo de ruta (traceroute).
- **-Pn**: Esta opción le dice a Nmap que no haga un "ping" previo a los hosts para ver si están activos. Por defecto, Nmap hace un ping para determinar si un host está activo antes de escanearlo. Con -Pn, Nmap escaneará los puertos incluso si el host no responde a los pings.

<p align="center">
<img src="/assets/images/MaquinaHeadless/Aspose.Words.c51fa9d9-6a10-477b-b35c-8f7240e81596.005.png">
</p>


En esta captura podemos ver algo interesante, primero que nada, podemos ver que en el puerto 22 si bien nos muestra la versión en el cual está trabajando el problema radica que no hay vulnerabilidad aparente, es decir si va al internet no hay ningún tipo de exploit que se puede usar para conectarse, así que el único puerto que queda disponible es el 5000 sin embargo este solo se usa para alojar el acceso a la página web así que no hay manera de explotar una vulnerabilidad. 

Solo queda ingresar a la página:

<p align="center">
<img src="/assets/images/MaquinaHeadless/Aspose.Words.c51fa9d9-6a10-477b-b35c-8f7240e81596.004.png">
</p>

En este caso procedemos a buscar páginas que puedan estar ocultas apartir de la URL, para eso usamos FUZZ

<p align="center">
<img src="/assets/images/MaquinaHeadless/Aspose.Words.c51fa9d9-6a10-477b-b35c-8f7240e81596.003.png">
</p>










