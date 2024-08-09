---
layout: single
title: Personalización de un entorno de trabajo Linux.
excerpt: "En este post es mi personalización personal de un sistema operativo Linux de las herramientas más usadas y las más cómodas."
date: 2024-07-9
classes: wide
header:
  teaser: assets/images/PersonalizacionLinux/painter-penguin.svg
  teaser_home_page: true
categories:
  - Linux
tags:
  - Linux
  - Personalización
---


# Personalización de Linux
Instalación de  [ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) para eso vamos a usar el siguiente comando:

- Debian o Ubuntu 
  ```sh
  sudo apt install zsh
  ```
- ArchLinux
  ```sh
  sudo apt -S zsh
  ```
Opcionalmente, se puede instalar [oh-my-zsh](https://ohmyz.sh/)

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Powerlevel10k
El tema preferido para la terminal es [powerlevel10k](https://github.com/romkatv/powerlevel10k)

Guía de instalación.
- Fuentes que se deben instalar:
  - **MesloLGS** fuentes que recomienda el autor:
     - [MesloLGS NF Regular.ttf](
         https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
     - [MesloLGS NF Bold.ttf](
         https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
     - [MesloLGS NF Italic.ttf](
         https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
     - [MesloLGS NF Bold Italic.ttf](
         https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf)
  - **Hack Nerd Fonts**
    - [Hack Nerd Fonts](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/Hack.zip)
      - Instalación manual funciona en cualquier distribución 
          ```sh 
          sudo mv Hack.zip /usr/share/fonts
          cd /usr/share/fonts
          sudo unzip Hack.zip
          sudo rm Hack.zip
          ``` 
      - Instalación automática en ArchLinux 
        ```sh
        yay -S ttf-hack-nerd
        ```

- Instalación 
    - Manual:
    ```sh
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
    echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
    ```
    - Usando Oh My Zsh
    ```sh
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
    ```
    En el archivo ``` ~/.zshrc ``` se debe agregar el tema en el caso de a ver usado Oh My Zsh ``` ZSH_THEME="powerlevel10k/powerlevel10k"```

    - Para restaurar ZSH se debe usar el siguiente comando: 
    ```sh 
    exec zsh
    ```
    - Para modificar el tema se usa:
    ```sh
    p10k configure
    ```

## Instalación de plugins
Hay dos plugin muy usados cuáles son: 
- zsh-autosuggestions
```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
- zsh-syntax-highlighting
```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting 
```

En el archivo ```.zshrc ``` se modificará lo siguiente:

```sh
plugins=(git
    zsh-autosuggestions
    zsh-syntax-highlighting 
)
```
Finalmente tendremos la siguiente terminal y nos quedaría de la siguiente manera:
<p align="center">
<img src="/assets/images/PersonalizacionLinux/ventana.png">
</p>

## Configuración de alias  

### Alias de bat
En este caso se utiliza la herramienta [bat](https://github.com/sharkdp/bat) la cual tiene una función parecida al comando cat, sin embargo, este tiene una presentación más elegante y más visual, por lo cual se opta por modificar el comando cat usando el alias en ```.zshrc```

## Instalación de la herramienta

Para la instalación de esta herramienta, se puede usar uno de los siguientes métodos:

### En Ubuntu/Debian:
1. Instalación mediante el gestor de paquetes:
    ```sh
    sudo apt install bat
    ```
2. Instalación manual descargando la [última versión](https://github.com/sharkdp/bat/releases/tag/v0.24.0):
    ```sh
    sudo apt install ./nombre_del_archivo.deb
    ```

### En Arch Linux:
1. Instalación mediante el gestor de paquetes `pacman`:
    ```sh
    sudo pacman -S bat
    ```
2. Instalación manual desde el AUR utilizando un ayudante como `yay`:
    ```sh
    yay -S bat
    ```


Dentro del archivo ```.zshrc``` se agrega el siguiente alias: 
```sh
alias cat='/bin/bat'
alias catn='/bin/cat'
alias  catln='/bin/bat --paging=never'
```
Así es como se ve nuestra terminal usando esta herramienta:
<p align="center">
<img src="/assets/images/PersonalizacionLinux/batcat.png">
</p>
En algunos casos se necesita copiar cosas de la terminal, así que para eso se configuró otro alias como catn
<p align="center">
<img src="/assets/images/PersonalizacionLinux/batcat2.png">
</p>

### Alias de lsd

`lsd` es una versión mejorada del comando `ls`, que incluye colores y otros elementos visuales para mejorar la experiencia de usuario. A continuación, se presentan alias que puedes agregar a tu archivo `.zshrc` para sustituir el uso de `ls` por `lsd`:

## Instalación de la herramienta

### En Ubuntu/Debian:
1. Instalación mediante el gestor de paquetes:
    ```sh
    sudo apt install lsd
    ```
2. Instalación manual descargando la [última versión](https://github.com/Peltoche/lsd/releases):
    ```sh
    sudo dpkg -i ./nombre_del_archivo.deb
    ```

### En Arch Linux:
1. Instalación mediante el gestor de paquetes `pacman`:
    ```sh
    sudo pacman -S lsd
    ```
2. Instalación manual desde el AUR utilizando un ayudante como `yay`:
    ```sh
    yay -S lsd
    ```

Dentro del archivo `.zshrc` se agregan los siguientes alias:
```sh
alias ls='lsd'
alias l='ls -l'
alias la='ls -a'
alias lla='ls -la'
alias lt='ls --tree'

```
Así es como se ve nuestra terminal usando esta herramienta:

<p align="center">
<img src="/assets/images/PersonalizacionLinux/carpetas.png">
</p>

<p align="center">
<img src="/assets/images/PersonalizacionLinux/l.png">
</p>



## Configuración de .zshrc
Esta es la configuración final `.zshrc`  

```sh

if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

# Path to your Oh My Zsh installation.
export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="powerlevel10k/powerlevel10k"
plugins=(git
    zsh-autosuggestions
    zsh-syntax-highlighting 
)

source $ZSH/oh-my-zsh.sh

# User configuration
ZSH_HIGHLIGHT_HIGHLIGHTERS=(main brackets pattern cursor)
ZSH_HIGHLIGHT_STYLES[command]='fg=blue,bold'
ZSH_HIGHLIGHT_STYLES[builtin]='fg=green,bold'

# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"

alias ls='lsd'
alias l='ls -l'
alias la='ls -a'
alias lla='ls -la'
alias lt='ls --tree'

alias cat='/bin/bat'
alias catn='/bin/cat'
alias  catln='/bin/bat --paging=never'

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh
```
## Aplicación para el usuario root
Si deseas que estos alias también estén disponibles para el usuario root, puedes seguir los mismos pasos anteriores. Alternativamente, puedes crear un enlace simbólico del archivo .zshrc de tu usuario hacia el directorio del root:

```sh
sudo ln -s ~/.zshrc /root/.zshrc
```
Si encuentras un error al crear el enlace, es posible que ya exista un archivo .zshrc en el directorio del root. En ese caso, puedes eliminar el archivo .zshrc del root y luego intentar nuevamente:

```sh
sudo rm /root/.zshrc 
```
Para mejorar la visibilidad y distinguir fácilmente en qué usuario estás, puedes personalizar el color del prompt. Esto se puede lograr editando el archivo `.p10k.zsh` de la siguiente manera:

<p align="center">
<img src="/assets/images/PersonalizacionLinux/root.png">
</p>

En el archivo `.p10k.zsh`, busca la línea 220, donde por defecto verás el valor `31`. Reemplaza este valor con la palabra `red`. De manera similar, en la línea 230, sustituye el valor `39` también por `red`.

Cerrando la terminal o saliendo del usuario root tendríamos de la siguiente manera:

<p align="center">
<img src="/assets/images/PersonalizacionLinux/root2.png">
</p>