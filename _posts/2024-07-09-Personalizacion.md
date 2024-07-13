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

```sh
apt install zsh
```
Opcionalmente, se puede instalar [oh-my-zsh](https://ohmyz.sh/)

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Powerlevel10k
El tema preferido para la terminal es [powerlevel10k](https://github.com/romkatv/powerlevel10k)

Guía de instalación.
- Fuentes que se deben instalar: 
   - [MesloLGS NF Regular.ttf](
       https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
   - [MesloLGS NF Bold.ttf](
       https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
   - [MesloLGS NF Italic.ttf](
       https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
   - [MesloLGS NF Bold Italic.ttf](
       https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf)
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



## Alias de bat
En este caso se utiliza la herramienta [bat](https://github.com/sharkdp/bat) la cual tiene una función parecida al comando cat, sin embargo, este tiene una presentación más elegante y más visual, por lo cual se opta por modificar el comando cat usando el alias en ```.zshrc```

Para la instalación de esta herramienta se puede instalar con el siguiente comando. 
```sh
sudo apt install bat
```
o bien se puede descargar la [última versión](https://github.com/sharkdp/bat/releases/tag/v0.24.0) para ello se instala de la siguiente manera.
```sh
sudo apt install ./nombre_del_archivo.deb
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


## Alias de lsb

```sh
alias ls='lsd'
alias l='ls -l'
alias la='ls -a'
alias lla='ls -la'
alias lt='ls --tree'
```

## Configuración personal de .zshrc

```sh

if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="powerlevel10k/powerlevel10k"

#alias 
alias cat='/bin/bat'
alias catn='/bin/cat'
alias  catln='/bin/bat --paging=never'

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

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh


eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
# Instalar gemas en ~/.gem
export GEM_HOME="$HOME/.gem"
export PATH="$HOME/.gem/bin:$PATH"
```
