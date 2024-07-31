---
layout: single
title: Instalación, configuración y personalización de ArchLinux.
excerpt: "Nos sumergimos en la instalación de Arch Linux, un proceso que puede parecer un gran reto al principio, pero que en realidad es muy sencillo. Además, la personalización del sistema abre un mundo de posibilidades, permitiéndote adaptar cada detalle a tus necesidades y preferencias."
date: 2024-07-19
classes: wide
header:
  teaser: assets/images/ArchLinux/icons8-arch-linux-480.png
  teaser_home_page: true
categories:
  - Linux
tags:
  - Linux
  - Personalización
---

## Arch Linux

<p style="text-align: justify;">
    <img src="/assets/images/ArchLinux/icons8-arch-linux-480.png" style="float: left; margin: 0 5px 0 0; width: 90px; height: auto;">
    Arch Linux es una distribución de Linux de propósito general x86-64 desarrollada de forma independiente. Se esfuerza por proporcionar las últimas versiones estables de la mayoría del software, siguiendo un modelo de rolling-release. La instalación por defecto es intencionadamente mínima para que los usuarios puedan añadir solo los paquetes que necesiten.
</p>

<p style="text-align: justify;">
En este post se abordará la instalación de manera sencilla y la explicación de ciertos detalles que hay que tomar en cuenta a la hora de instalar el sistema. Una mala configuración y/o instalación puede terminar dañando las particiones si se está instalando junto con algún otro sistema operativo.
</p>

## Descarga
Para descargar Arch Linux, es necesario hacerlo desde su página oficial. No hay un enlace directo para descargar la ISO; en su lugar, se deben utilizar los enlaces Torrent o Magnet.

[Descarga de ArchLinux](https://archlinux.org/download/)

Podemos ver los enlaces mencionados anteriormente en el apartado **BitTorrent Download (recommended)**:

<p align="center">
<img src="/assets/images/ArchLinux/ArchPagina.png">
</p>

En este caso se descargo la version de Torrent, para poder descargar este archivo se puede usar [uTorrent](https://www.utorrent.com/) para Windows o **qBittorrent** para Linux

<p align="center">
<img src="/assets/images/ArchLinux/utorret.png">
</p>

## Instalación primera parte  
<p style="text-align: justify;"> 
Una vez descargada la ISO, procederemos a utilizar <a href="https://rufus.ie/es/">Rufus</a>, <a href="https://www.ventoy.net/en/download.html">Ventoy</a> u otro programa similar para grabar la imagen en una memoria USB. Alternativamente, también puedes utilizar la ISO para instalar el sistema en una máquina virtual.

Una vez que hayamos iniciado el sistema, ya sea en la máquina virtual o de manera nativa, nos aparecerá una ventana como la siguiente:

<p style="text-align: center;">
<img src="/assets/images/ArchLinux/EFFI.png">
</p>
<p style="text-align: justify;">

Seleccionaremos la primera opción y presionaremos Enter para iniciar Arch Linux:

</p>
<p style="text-align: center;">

<img src="/assets/images/ArchLinux/bienvenida.png">
</p>
</p>
<p style="text-align: justify;"> 
Una vez que estemos en la pantalla de bienvenida, estaremos directamente como el usuario root. Lo primero que haremos es usar un comando para configurar el teclado en español. Si no realizamos este paso, el teclado estará configurado en inglés. En caso de contar con un teclado en inglés, no debería representar ningún problema. De lo contrario, utilizaremos el siguiente comando:
</p>

```bash 
loadkey es
```
<h2 id="Configuracion-de-los-discos"> Configuración de los discos</h2>
<p style="text-align: justify;">
<strong>Nota:</strong> Si se está instalando de manera nativa y se tiene instalado otro sistema operativo como Windows, es necesario hacer los siguientes pasos. De lo contrario, se pueden <a href="#instalacion-segunda-parte">omitir</a>.
</p>
<p style="text-align: justify;">
Para la instalación de Arch es necesario tener dos particiones, las cuales son muy importantes a la hora de instalar el sistema. Lo primero que haremos es usar el comando:

</p>


```sh
lsblk
```
<p style="text-align: justify;">
El comando anterior nos muestra un listado de los discos que tenemos en nuestro sistema. Es recomendable particionar el disco de antemano, ya sea usando el gestor de discos de Windows o alguna herramienta de Linux si se tiene una partición previa.
Una vez hecho esto, procederemos a usar el siguiente comando:
</p>


```sh
cfdisk
```
<p style="text-align: justify;">
Ejemplo de los comandos mencionados anteriormente:
</p>
<p style="text-align: center;">
<img src="/assets/images/ArchLinux/ConfDisk.png">
</p>
<p style="text-align: justify;">
Al ejecutar el comando nos aparece lo siguiente:
</p>
<p style="text-align: center;">
<img src="/assets/images/ArchLinux/gpt.png">
</p>
<p style="text-align: justify;">
Seleccionamos GPT y presionamos Enter. Esto nos llevará a la interfaz de nuestro disco, donde podremos ver todas nuestras particiones. Es importante destacar que cualquier cambio realizado debe ser verificado varias veces antes de escribir los cambios, ya que esto puede dañar las demás particiones. El espacio que vayamos a usar debería aparecer con la leyenda <strong style="color: green;">"Free space"</strong>. Como se mencionó anteriormente, este paso debe realizarse desde otro sistema. Cabe aclarar que esto no aplica si se va a instalar Arch en todo el disco.
</p>
<p style="text-align: justify;">
Con <strong>Resize</strong> le quitamos 1 GB al disco a utilizar. Esta partición de 1 GB, con <strong>Type</strong>, se debe seleccionar <strong>EFI System</strong>. La partición de mayor volumen debe tener el tipo <strong>Linux filesystem</strong>. Al final, deberíamos tenerlo de esta manera:
</p>
<p style="text-align: center;">
<img src="/assets/images/ArchLinux/discos.png">
</p>
<p style="text-align: justify;">
Para aguardar los cambios es necesario seleccionar <strong>Write</strong> y aceptar los cambios
</p>

<h2 id="instalacion-segunda-parte">Instalación segunda parte</h2>

Continuando con la instalacion procedemos a usar el siguiente comando:
```sh
archinstall
```
**Nota**: es necesario tener internet para ejecutar este comando

Se nos desplegará lo siguiente:

<p style="text-align: center;">
<img src="/assets/images/ArchLinux/archinstall.png">
</p>
<p style="text-align: justify;">
Aquí es totalmente personalizable, y se deben tomar en cuenta los siguientes datos:
</p>
<ol style="text-align: justify;">
  <li><strong>Lenguaje</strong>: Puedes dejarlo en inglés o cambiarlo a español.</li>
  <li><strong>Mirrors</strong>: Son servidores que alojan los paquetes de software y las actualizaciones del sistema. Aquí puedes seleccionar el país de procedencia.</li>
  <li><strong>Locales</strong>: Aquí se selecciona la distribución del teclado. Si es inglés, puede ser <code>en_US</code>; y si es español, puede ser <code>es_MX</code> para México o <code>es_ES</code> para España. La opción puede variar dependiendo del país.</li>
  <li><strong>Configuración de discos</strong>: Aquí se desplegarán las siguientes opciones:
  <p style="text-align: center;">
<img src="/assets/images/ArchLinux/MVe.png" alt="Configuración de discos">
</p>

<ul>
  <li>La primera opción se utiliza cuando se está usando una máquina virtual o cuando se desea hacer una instalación limpia en un equipo, eliminando todos los datos previos. Al seleccionar esta opción, se mostrará cómo será particionado y formateado el disco. Se debe seleccionar el formato <code>ext4</code> y guardar los cambios.</li>
  <li>La segunda opción consiste en una instalación manual y se aplica solo si ya tienes otro sistema operativo instalado. Para ello, los discos deben estar previamente <a href="#Configuracion-de-los-discos">configurados</a>. Al seleccionar esta opción, aparecerá la siguiente ventana:
  <p style="text-align: center;">
  <img src="/assets/images/ArchLinux/manual2.png" alt="Configuración manual">
  </p>
  Las propiedades que deben tener los discos son:
  <ul>
      <li>Disco de 1 GB
        <ul>
          <li>Asignación de punto de montaje: <code>/boot</code></li>
          <li>Formato: <code>Fat32</code></li>
        </ul>
      </li>
      <li>Disco de mayor tamaño
        <ul>
          <li>Asignación de punto de montaje: <code>/</code></li>
          <li>Formato: <code>ext4</code></li>
        </ul>
      </li>
    </ul>

  Finalmente, deberíamos tenerlo de esta manera:

  <p style="text-align: center;">
    <img src="/assets/images/ArchLinux/manual3.png" alt="Configuración final">
    </p>
    
  Confirma los cambios y sal del menú.</li>
</ul>
  </li>
  <li><strong>Bootloader</strong>: Se deja por defecto en GRUB.</li>
  <li><strong>Swap</strong>: Se deja por defecto en True.</li>
  <li><strong>Hostname</strong>: Se puede modificar al otro nombre o se deja por defecto</li>
  <li><strong>Root password</strong>: Se establece una contraseña exclusiva para root</li>
   <li><strong>User account </strong>: Se crea una cuenta de usuario aparte del usuario root. Esta cuenta requerirá un nombre de usuario y una contraseña. Además, esta cuenta se añadirá al grupo de wheel para permitir permisos administrativos.</li>
  <li><strong>Profile</strong>: En esta opción, seleccionamos el entorno gráfico. Aquí podemos elegir entre diferentes entornos de escritorio, como los más conocidos: GNOME, KDE Plasma, entre otros. Asimismo, podemos seleccionar el gestor de inicio de sesión, como GDM, SDDM, etc.</li>
  <li><strong>Audio</strong>: En esta opción, puedes seleccionar cualquiera de las opciones disponibles, ya que todas funcionan correctamente.</li>
  <li><strong>Kernel</strong>: Se queda como esta en Linux se tienes mas conocimiento del tema puede seleccionar al gusto.</li>
  <li><strong>Networking Configuration</strong>: Selecciona la opción de NetworkManager. Es importante que no dejes esta opción sin seleccionar, ya que, de lo contrario, no podrás conectarte a Internet.</li>
  <li><strong>Timezone</strong>: Se selecciona la zona horaria.</li>
  <li><strong>Automatic time sync</strong>: Se deja en true.</li>
 
  <li><strong>Optional repositories</strong>: Se puede omitir esta opción</li>
 </ol>

<p style="text-align: justify;">
Una vez seleccionada la opciones adecuadas lo tendremos de la siguiente manera:
</p>

<p style="text-align: center;">
<img src="/assets/images/ArchLinux/Archinstall2.png" >
</p>

<p style="text-align: justify;">
Selecciona la opción de Instalar. Una vez que comience el proceso, se iniciará una cuenta regresiva. Al finalizar esta cuenta regresiva, presiona Enter para comenzar la instalación.
</p>
<p style="text-align: justify;">
La instalación puede llevar algo de tiempo asi que solo queda esperar. Si todo sale bien nos debe aparecer la siguiente pantalla:     
</p>

<p style="text-align: center;">
<img src="/assets/images/ArchLinux/finalidad.png" >
</p>
<p style="text-align: justify;">
En esta opción se debe seleccionar no y dar enter para salir.
</p>

<p style="text-align: justify;">
Para comenzar comenzar nuestro ArchLinux se coloca el siguiente comando para reiniciar el sistema:
</p>

```sh
reboot
```
<p style="text-align: justify;">
Cuando se reinicie, debe aparecer el gestor de inicio de sesión con el nombre de usuario que configuraste previamente. Ingresa la respectiva contraseña. Una vez iniciada tu sesión, deberías ver tu escritorio.
</p>

<p style="text-align: center;">
<img src="/assets/images/ArchLinux/escritorio.png" >
</p>
<p style="text-align: center;">
<img src="/assets/images/ArchLinux/neo.png" >
</p>

## Herramientas
Actualización del sistema:

```sh
sudo pacman -Syu
```
Instalación de herramientas:
- Instalación de Git
  ```sh
  sudo pacman -S git 
  ```
- Instalación de kitty (Terminal):
  ```sh
  sudo pacman -S kitty
  ```
- Instalación de Firefox (Navegador)
  ```sh
  sudo pacman -s firefox
  ```
- Instalación de Yay (AUR Helper):
  - Primero, instala los paquetes necesarios para compilar Yay:
  ```sh
  sudo pacman -S base-devel
  ```
  - Clona el repositorio de Yay:
  ```sh
  git clone https://aur.archlinux.org/yay.git
  ```
  - Navega al directorio clonado e instala Yay:
  ```sh
  cd yay
  makepkg -si
  ```
- htop (Monitor del sistema interactivo):
  ```sh
  sudo pacman -S htop
  ```
- neofetch (Información del sistema)
  ```sh
  sudo pacman -S neofetch
  ```
- vim y neovim (Editor de texto avanzado):
  ```sh
  sudo pacman -S vim neovim
  ```
- nano (Editor de texto simple)
  ```sh
  sudo pacman -S nano
  ```
- Visual Studio Code (Editor de código fuente)
  ```sh
  yay -S visual-studio-code-bin
  ```
- VLC (Reproductor multimedia)
  ```sh
  sudo pacman -S vlc
  ```
- wget y curl (Herramienta de descarga):
  ```sh
  sudo pacman -S wget curl
  ```





## Personalización
La personalización puede variar dependiendo de cada escritorio. En este caso, se usará KDE Plasma, que es un escritorio bastante personalizable.

<p style="text-align: center;">
<img src="/assets/images/ArchLinux/Personalizacion.png" >
</p>

Personalización de nano para que tenga color usaremos [nanorc](https://github.com/scopatz/nanorc)
```sh
curl https://raw.githubusercontent.com/scopatz/nanorc/master/install.sh | sh
```
Personalizacion de neovim usaremos [NvChad](https://github.com/NvChad/NvChad?tab=readme-ov-file)

```sh
git clone https://github.com/NvChad/starter ~/.config/nvim && nvim
```
Para mas detalles de instalación de herramientas para Linux podemos ver el siguiente enlace: 

[Personalización de un entorno de trabajo Linux](https://eduardo99rp.github.io/linux/ArchLinux/)


