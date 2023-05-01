# Installation de octobercms avec docker.

> **Nous avons besoin de Ubuntu : Linux terminal**
>
> _1,2,3,4_.

- Envie de connaître le projet final **lien du site web** [^1]

[^1]: [Voici le lien du projet](https://administration-dashboard.herokuapp.com/#/)

## Table de matière

- [Installation de octobercms avec docker.](#installation-de-octobercms-avec-docker)
  - [Table de matière](#table-de-matière)
  - [Introduction](#introduction)
  - [Mise en place](#mise-en-place)
    - [Mise en place avec ubuntu \& docker.](#mise-en-place-avec-ubuntu--docker)
- [Install Nginx.](#install-nginx)
- [Define mountable directories.](#define-mountable-directories)
- [Define working directory.](#define-working-directory)
- [Define default command.](#define-default-command)
- [Deux solution pour indique une commande à shell qui vient du terminal(cmd)](#deux-solution-pour-indique-une-commande-à-shell-qui-vient-du-terminalcmd)
  - [1 :](#1-)
  - [2 : Les commande CMD ont va les réécrire entièrement : cette méthode va dépendre de l'ordre de commande sur le dockerfile.](#2--les-commande-cmd-ont-va-les-réécrire-entièrement--cette-méthode-va-dépendre-de-lordre-de-commande-sur-le-dockerfile)
- [exemple 1 : changer le entrypoint sur dockerfile:](#exemple-1--changer-le-entrypoint-sur-dockerfile)
- [Exemple 2 : Changer les entrypoint sur le dockerfile et le action.yml à même temps:](#exemple-2--changer-les-entrypoint-sur-le-dockerfile-et-le-actionyml-à-même-temps)
    - [**Running CLI commands in the container**](#running-cli-commands-in-the-container)
      - [Création du router authentification pour la page authentification.](#création-du-router-authentification-pour-la-page-authentification)
    - [Pour me connecter à mysql du network de la database du flutter\_docker](#pour-me-connecter-à-mysql-du-network-de-la-database-du-flutter_docker)
- [Pour Simplifier les choses : il faut utiliser docker-compose.yml quand nous utilisons les multi-containers : Nous pouvons écrire une séries de commandes pour écrire les commandes que normalement nous devons l'écrire à la chaines manuellement.](#pour-simplifier-les-choses--il-faut-utiliser-docker-composeyml-quand-nous-utilisons-les-multi-containers--nous-pouvons-écrire-une-séries-de-commandes-pour-écrire-les-commandes-que-normalement-nous-devons-lécrire-à-la-chaines-manuellement)
    - [**Accessing the MySQL database**](#accessing-the-mysql-database)
      - [Création du formulaire de validation d’enregistrement \& registre de navigation.](#création-du-formulaire-de-validation-denregistrement--registre-de-navigation)
    - [**How to License a Container**](#how-to-license-a-container)
      - [Open in vs code : Remote-Containers: Attach to running container](#open-in-vs-code--remote-containers-attach-to-running-container)
  - [Use container vscode-server with conter online to codding anywhere.](#use-container-vscode-server-with-conter-online-to-codding-anywhere)
- [OpenVSCode Server](#openvscode-server)
  - [What is this?](#what-is-this)
  - [Why?](#why)
  - [Getting started](#getting-started)
    - [Docker](#docker)
      - [Custom Environment](#custom-environment)
      - [Pre-installing VSCode extensions](#pre-installing-vscode-extensions)
    - [Linux](#linux)
    - [Securing access to your IDE](#securing-access-to-your-ide)
    - [Deployment guides](#deployment-guides)
  - [The scope of this project](#the-scope-of-this-project)
  - [Documentation](#documentation)
  - [Supporters](#supporters)
  - [Contributing](#contributing)
  - [Community \& Feedback](#community--feedback)
  - [Legal](#legal)
    - [**Section 10**](#section-10)
      - [Backend pour le panel d'administration.](#backend-pour-le-panel-dadministration)
    - [**Section 11**](#section-11)
      - [Authentication et protection des routes.](#authentication-et-protection-des-routes)
    - [**Section 12**](#section-12)
      - [Créer le UI de la view Catégorie et lier le Backend de notre API à la page web.](#créer-le-ui-de-la-view-catégorie-et-lier-le-backend-de-notre-api-à-la-page-web)
    - [**Section 13**](#section-13)
      - [Optimisation des routes pour éviter que notre application se redessine à tout moment.](#optimisation-des-routes-pour-éviter-que-notre-application-se-redessine-à-tout-moment)
    - [**Section 14**](#section-14)
      - [Gestion des utilisateurs de l'application.](#gestion-des-utilisateurs-de-lapplication)
    - [**Section 15**](#section-15)
      - [Télécharger des fichiers dans le backend et le lier avec Cloudinary et Déploiement de la version de notre application sur le web avec Heroku.](#télécharger-des-fichiers-dans-le-backend-et-le-lier-avec-cloudinary-et-déploiement-de-la-version-de-notre-application-sur-le-web-avec-heroku)
- [Utilisation des outils suivant :](#utilisation-des-outils-suivant-)

---

## Introduction

Nous allons installer Octobercms grâce à Docker et au terminal de Linux : Ubuntu . Pour en savoir plus sur le créateur [Sergio Nino](https://github.com/Sergioanino).

![screenshot.png](assets/screenshot.PNG)

---

## Mise en place

Aller sur Github et télécharger le projet avec un **clone** ou avec le **ZIP** [admin_dashboard](https://github.com/Sergioanino/admin_dashboard).

### Mise en place avec ubuntu & docker.

`Obtenez-le en exécutant la commande suivante pour obtenir les dépendances:`
`Il faut ouvrir la power shell avec mode admin:`

```
wsl --install
wsl --install -d <DistroName> : To change the distribution installed.
```

```
wsl -l -v : listing the distribution

-l = --list
-v = --verbose
-o = --online
-d = --distribution
-s = --set-default-version
-r = --running
-1 = --quiet

wsl -s Debian : to set the default distribution to Debian. Now running wsl npm init from Powershell will run the npm init command in Debian.

Change directory to home
The ~ can be used with wsl to start in the user's home directory. To jump from any directory back to home from within a WSL command prompt, you can use the command: cd ~.

wsl ~
```

```
wsl --set-default-version 2
```

```
wsl --set-version Ubuntu 2

From Windows Command Prompt or PowerShell, you can open your default Linux distribution inside your current command line, by entering:

wsl.exe.

If you want to install additional distributions from inside a Linux/Bash command line (rather than from PowerShell or Command Prompt), you must use .exe in the command: wsl.exe --install -d <Distribution Name> or to list available distributions:

wsl.exe -l -o

Run a specific Linux distribution from PowerShell or CMD.
To run a specific Linux distribution with a specific user, replace <Distribution Name> with the name of your preferred Linux distribution (ie. Debian) and <User Name> with the name of an existing user (ie. root).

wsl --distribution <Distribution Name> --user <User Name>

Update WSL :
wsl --update

Check WSL status :
wsl --status

Run as a specific user : sh
wsl -u <Username>`, `wsl --user <Username>

Change the default user for a distribution : sh
<DistributionName> config --default-user <Username>

Shutdown : sh
wsl --shutdown

Terminate : sh
wsl --terminate <Distribution Name>

Export a distribution to a TAR file : sh
wsl --export <Distribution Name> <FileName>

we want to know more : https://docs.microsoft.com/en-us/windows/wsl/basic-commands

Next étapes : https://docs.microsoft.com/en-us/windows/wsl/setup/environment#set-up-your-linux-username-and-password

Next étapes :
https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-git

```

Les containers vont juste vivre pendant l'execution d'un processus en particulier et s'arrêter par la suite :

Le DOCKERFILE :
Exemple de docker images - Nginx

# Install Nginx.

RUN \
 add-apt-repository -y ppa:nginx/stable && \
 apt-get update && \
 apt-get install -y nginx && \
 rm -rf /var/lib/apt/lists/\* && \
 echo "\ndaemon off;" >> /etc/nginx/nginx.conf && \
 chown -R www-data:www-data /var/lib/nginx

# Define mountable directories.

VOLUMES ["/etc/nginx/sites-enabled", "/etc/nginx/certs", ....]

# Define working directory.

WORKDIR /etc/nginx

# Define default command.

CMD ["nginx"] : commande default to the image the [nginx]

info : Quand on fait courir une image de [ubuntu] sur la commande CMD ["bash"] : il faut tenir compte que les commande sur les terminals ne sont pas de processus comme un service cloud et de serveur DATABASE. Souvent un service sur va lire en Shell vont écouter un [inputs] du terminal et s'il ne trouve pas le terminal, il arrête d'execution.

!!!!!! CMD vs ENTRYPOINT

# Deux solution pour indique une commande à shell qui vient du terminal(cmd)

## 1 :

en: append a commande to the docker run command and that way it overrides the default command specified withing the image int this case. fr:
Ajoutez une commande à la commande docker run et de cette façon, elle remplace la commande par défaut spécifiée dans l'image dans ce cas.

Exemple : docker run ubuntu [COMMAND] - docker run ubuntu sleep 5

Comment peut-t-on créer une image permanentent au moment de partir pour vouloir créer notre propre image.

FROM Ubuntu
CMS sleep 5

Il faut seulement lui spécifier une commande de plus.

shell format json format
CMD commande param1--------------|-----CMD sleep 5
CDM ["command", "param1"]--------|-----CMD ["sleep", "5"]

Important il faut mettre "" entre chaque espace.

- docker build -t ubuntu-sleeper .
- docker run ubuntu-sleeper

Exemple :

- dockerfile :

  FROM Ubuntu
  CMD sleep 5

Terminal : docker run ubuntu-sleeper sleep 10

- Command at Startup: sleep 10

- dockerfile :

  FROM Ubuntu
  ENTRYPOINT ["sleep"]

terminal : docker run ubuntu-sleeper 10

- Command at Startup: sleep 10

sleep 10 : vient du [Entrypoint] et le 10 de la commande sur le terminal sleeper [10]

## 2 : Les commande CMD ont va les réécrire entièrement : cette méthode va dépendre de l'ordre de commande sur le dockerfile.

exemple :

FROM Ubuntu
ENTRYPOINT ["sleep"]
CMD ["5"]

terminal : docker run ubuntu-sleeper

- Command at Start: sleep 5

terminal : docker run ubuntu-sleeper 10

- Command at Startup: sleep 10

Ce qu'on va écrire sur le [terminal] : va sur écrire la commande CMD.

# exemple 1 : changer le entrypoint sur dockerfile:

terminal : docker run --entrypoint sleep2.0 ubuntu-sleeper 10

- Commande at Startup : sleep2.0 10

# Exemple 2 : Changer les entrypoint sur le dockerfile et le action.yml à même temps:

- Dockerfile
  FROM Ubuntu
  ENTRYPOINT ["sleep"]
  CMD ["5"]

- pod-action.yml
  apiVersion : v1
  kind: Pod
  metadata:
  --name: ubuntu-sleeper-pod
  spec:
  --containers:
  .....-name: ubuntu-sleeper
  ------image: ubuntu-sleeper
  ------command:["sleeper"]
  ------args: ["10"]

- Terminal :
  docker run --name ubuntu-sleeper \
  .....--entrypoint sleep2.0
  .....ubuntu-sleeper 10

<!-- info : La commande sur le terminal => avec le entrypoint va modifier la commande sur l'action yml à l'endroit commande -->

Summarize there are two fields that correspond to two instructions in the dockerfile the commande field overrides the entry point instruction. The args field overrides the command instruction in the dockerfile. remember it's not the command field that overrides the CMD instruction in the dockerfile.

En résumé, il y a deux champs qui correspondent à deux instructions dans le Dockerfile : le champ [command]remplace l'instruction point d'entrée. le champ [args] remplace l'instruction command dans le fichier docker. rappelez-vous que ce n'est pas le champ command qui remplace l'instruction CMD dans le Dockerfile.

<!-- ? info :  -->

Il existe trois manière de faire courir l'image

```
lsb_release -a
```

```
docker
```

```
ubuntu config --default-user root
```

```
mkdir -p /var/october/october_docker
cd /var/october/october_docker
```

```
bash -c "$(curl https://octobercms.com/api/dockerdevinstaller)"
```

```
default :8080 & 3333
```

```
code for open vscode : open de file !
```

```
\\wsl$\Ubuntu\var\october\october_docker
```

```
\\wsl$\Ubuntu\var\october\october_docker
```

---

### **Running CLI commands in the container**

#### Création du router authentification pour la page authentification.

- Install the extension.
- Open the Command Palette (ctrl+shift+p) and select Docker - Containers: Attach Shell.
- Select your container.
- That will open the Terminal panel attached to the container.

```
php artisan
```

```
./october-docker-install.sh
```

---

Sur le terminal :

1 : Connaître la version de docker : #7
docker --version ou docker -v

2 : Partir un container à partir d'un image : d'un projet sur le dockerHub - container des d'autres entreprise exemple : node.js et php: image !

- Docker pull : télécharge l'image mais ne va pas la faire courir.
  docker pull mysql

- Docker run : va faire courir l'image qui va se convertir dans un container.
  docker run <nom du container dockerHub>: <pour mettre un tag de la version>

exemple : docker run mysql:latest

\*\* : -e : Argument extra pour docker run : envoie un variable d'environnement pour le configurer.

Start a mysql server instance
Starting a MySQL instance is simple:

$ docker run --name <some-mysql> -e MYSQL_ROOT_PASSWORD=<my-secret-pw> -d mysql:tag -p <8080(externe):3030(interne)>

exemple : docker run --name <server_image_container> sergio_image -p 8080:3030

... where some-mysql is the name you want to assign to your container, my-secret-pw is the password to be set for the MySQL root user and tag is the tag specifying the MySQL version you want. See the list above for relevant tags.

3 : Créer un package json pour simplifier les images : container : FONCTIONNE : sur windows avant de créer un container.
nmp init -y

4 : Connaître les Images installer sur docker, et qui peuvent courir aussi sur l'ordinateur.

- add : | head - pour montrer seulement les derniers images.
  docker images ou docker images | head

5 : Connaître les containers qui courts dans mon ordinateur.
docker ps
docker ps -a : Il va nous montrer tous les containers run sur cette ordinateur.

ctrl+c sur un de container pour l'arrêter ou prendre le hashing du container avec la commande stop pour l'arrêter.
docker stop <hashing_container>

5.1 : Start un containers à partir d'un hashing :
docker start <hashing>

5.2 : Connaître les longing du container :
docker logs <hashing id container ou le nom du containers si specifier du moment de run le containers>

5.3 : Connaître le logs mais en attente de reception d'un log :
docker logs -f <hashing id>

% ! info : dans docker on écrit toujours en output ! Quand on fait docker logs on capture le container et l'image.

6 : RUN CMD & ENTRYPOINT différence : curl : c'est quoi ?

- run : run est pour lancer de commande au moment de construire l'image.

  -d : détacher le container pour le courir en background.

  docker run -d <nom de l'image>

- cmd : Les commandes qui vont s'executer par défaut au moment que tu run le container. exemple : pour courir un serveur : php,python & etc. En plus, nous pourrons sur-écrire une nouvelle commande pour écraser la commande par défaut, au moment de courir à nouveau l'image avec des commande extra : comme -it ou sh

- ENTRYPOINT : Les commandes vont être executer au moment d'initialiser le container sauf qu'il n'est pas créer pour qu'on l'utilise pour sur-écrire les commande, il est plus pour qu'il fonctionne comme un executable. Il est possible de le sur-écrire au moment de faire docker run avec de commande de plus.
  exemple : Il faut passer des arguments aux commande du container.

- exec va executer une commande à l'intérieur du container qui run déjà.

  -i : Une session interactif.
  -t : Émuler une terminal.

  sh : shell pour le terminal.

  docker exec -it <id hashing container> sh

  6.1 : Executer une image dans un container de manière interactive : De cette manière on rentre à l'intérieur d'un container!
  docker exec -it mymysql bash : exemple : docker exec -it sergio_image bash

- Cela va executer une bash sur notre système.

  6.2 : Voir les containers en execution. ps: show infos container execution.
  docker ps
  % Photo @lien assets

  6.1 Arrêter un container en execution.
  docker stop <hashing_container>

  6.2 Supprimer un container. arrêt du container avant suppression. rm: supprimer
  docker rm <hashing_container>

7 : 1er : Créer un dossier avec le nom : DockerFiles.

C'est quoi vim ? je crois que sa créer le dossier apres : - vim DockerFiles : Voir le fichier : DockerFiles pour la suite du Tuto.

7 : Créer un installateur de notre container avec tout les dépendes des apps pour le project.

    - docker build -t <nom du container> .<dit que ce sur ce folder est >

si nous voulons courir notre nouvelle image du container :

docker run <nom de l'image donné -t en haut>

    - Pour lui indique le port à courir au moment de run l'image pour le voir sur internet : -p 8080:3030

docker run -p 8080:3030 <nom de l'image>

ou -dp : mettre en veille l'écoute du log.

docker run -dp 8080:3030 <nom de l'image>

si nous voulons installer le thème et la console de zsh : sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

Pour persister les données ajouter au container et image de docker leur des ajouts sur la Database en ligne.

    - : - modification bidirectionnel

    - docker run -d -v /<path ou est installer notre image et container>:<url de l'image fin du path> -p 8080:3030 <nom image>

Pour persister des changements ou corriger des erreurs sans recréer l'image du container :

    - docker run -d -v /<path ou est installer notre image et container>:<url de l'image fin du path> -p 8080:3030 -v /<path ou est installer notre image et container/src>:<url de l'image fin du path du/src> <nom image>

    exemple : docker run -d -v /Users/Ubuntu/var/flutter/flutter_docker/app/etc:etc/todos -p 8080:3030 -v /Users/Ubuntu/var/flutter/flutter_docker/app/src:/app/src flutter_docker

- Après d'avoir persister tous les changements réaliser sur le container et l'image : nous pouvons re-créer l'image avec tous les nouveau changements :

docker build -t <nom-image>:v2 .

<!-- info : mettre l'image sur Dockerhub : repository public pour traduits -->

- Il faut bien tagues sont image: docker tag <id-img> <user-docker>/<nom-img>:v2

exemple : docker tag 123tagdocker456 sergioanino/flutter_docker:v2

- docker login
  add les user et le password du login :

- docker push sergioanino/flutter_docker:v2

<!-- info  : encore plus loin avec docker compose-->

<!-- :@ Docker Multi container :  -->
<!-- 52:04 min : https://www.youtube.com/watch?v=CV_Uf3Dq-EU&t=3406s&ab_channel=PeladoNerd -->

Il est nécessaire que plusieurs container courts sur la même "network"pour partager leur caractéristique.

exemple : c://flutter_docker/multi_container$ docker network create flutter_docker

1er : docker network create <nom-container-multi-container>

2e : c:\flutter_docker\multi-container$ docker run -d \

> --network flutter_docker --network-alias mysql \
> -v flutter_docker-mysql-data:/var/lib/mysql \
> -e MYSQL_ROOT_PASSWORD=secret \
> -e MYSQL_DATABASE=flutter_docker \
> mysql:5.7

Courir le network : docker exec -it <id-hashing-img-multi> mysql -p
Cela courir mysql -p à l'intérieur du container : <id_hashing-img-multi> à l'intérieur de ce container : il va utilise le binaire de mysql à l'intérieur du container pas celui de notre pc. need : password : le même que la commande en haut : secret.

show databases : à l'intérieur du container multi.

add new img : nicolaka/netshoot : va nous permette de nous connecter au network de notre environnement mysql du flutter_docker

- multi-container$ docker run -it --network <flutter_docker> nicolaka/netshoot

Par la suite il faut résoudre le problème de API du serveur local :
dig mysql - 52:43min

### Pour me connecter à mysql du network de la database du flutter_docker

docker run -dp 8080:3030 \

> --network flutter_docker \
> -e MYSQL_HOST=mysql \
> -e MYSQL_USER=root \
> -e MYSQL_PASSWORD=secret \
> -e MYSQL_DB=flutter_docker \
> flutter_docker:v2

docker ps : => voir images.

voir les logs : Voir que flutter_docker:v2 est connecter sur quelle port.

- Se connecter avec un autre mysql mais qui détient déjà tous la DB du projet et de mettre à jours les données dans les deux endroit sur la database.

docker run -dp 8080:3030 --network flutter_docker -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=secret -e MYSQL_DB=flutter_docker flutter_docker:v2

<!-- :@ Docker Multi container : fin  -->

# Pour Simplifier les choses : il faut utiliser docker-compose.yml quand nous utilisons les multi-containers : Nous pouvons écrire une séries de commandes pour écrire les commandes que normalement nous devons l'écrire à la chaines manuellement.

https://docs.docker.com/compose/

8 : Créer en 1er : le file - vim docker-compose.yaml &

info : sert à combiner plusieurs container dans une seule documents de dependence_dev

<!-- info : Après d'avoir écrit notre docker-compose faire la commande suivante pour lancer les commander créer par docker compose. -->

- d : détachement.
  c:/multi-container$ docker-compose up -d

9 : Créer l'image de docker-compose.env.dev.
docker-compose up

9.1 : docker logs <l'img du docker-compose>

9.2 : mettre à terre tout la network de compose : docker-compose down

10 : Créer un build du container en env.dev
docker-compose up --build

11 : Installer un autre environnement de développement en production.
docker-compose.prod.yml up

<!-- info : Création de volume et de port dans le docker-compose -->

pour se rendre à un bash -it : docker exec -it <id-hash> bash
commande à l'intérieur d'un bash : terminal pour installer : ps
ps fax
apt-get install ps

TODOS: 10;59

<!-- Photo @lien assets -->

### **Accessing the MySQL database**

#### Création du formulaire de validation d’enregistrement & registre de navigation.

- mysql -uroot -proot octobercms
- show tables;
- exit
- Alternatively, if you have the MySQL client tools installed on your host computer, you can connect from your host machine in Windows Command Prompt: mysql --host=127.0.0.1 -uroot -proot --port=3307 octobercms. The port argument is the port number you entered in the container configuration. The connection string was displayed in the interactive script output.

---

### **How to License a Container**

#### Open in vs code : Remote-Containers: Attach to running container

- Open file :
- Écrire le mots du file comme suit : /var/www/html
- Licence.

```
php artisan project:set LICENSE-KEY
```

```
composer reinstall '*'
```

```
php artisan cache:clear
```

---

## Use container vscode-server with conter online to codding anywhere.

1. Télécharger l'image de [openvscode-server](https://github.com/gitpod-io/openvscode-server). Si tu veux en savoir plus sur la documentation : du [package/librairie](https://github.com/gitpod-io/openvscode-server/tree/docs).

- Commende sur le terminal : 
```

```

# OpenVSCode Server

[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-908a85?logo=gitpod)](https://gitpod.io/from-referrer)
[![GitHub](https://img.shields.io/github/license/gitpod-io/openvscode-server)](https://github.com/gitpod-io/openvscode-server/blob/main/LICENSE.txt)
[![Discord](https://img.shields.io/discord/816244985187008514)](https://www.gitpod.io/chat)

## What is this?

This project provides a version of VS Code that runs a server on a remote machine and allows access through a modern web browser. It's based on the very same architecture used by [Gitpod](https://www.gitpod.io) or [GitHub Codespaces](https://github.com/features/codespaces) at scale.

<img width="1624" alt="Screenshot 2021-09-02 at 08 39 26" src="https://user-images.githubusercontent.com/372735/131794918-d6602646-4d67-435b-88fe-620a3cc0a3aa.png">

## Why?

VS Code has traditionally been a desktop IDE built with web technologies. A few years back, people started patching it in order to run it in a remote context and to make it accessible through web browsers. These efforts have been complex and error prone, because many changes had to be made across the large code base of VS Code.

Luckily, in 2019 the VS Code team started to refactor its architecture to support a browser-based working mode. While this architecture has been adopted by Gitpod and GitHub, the important bits have not been open-sourced, until now. As a result, many people in the community still use the old, hard to maintain and error-prone approach.

At Gitpod, we've been asked a lot about how we do it. So we thought we might as well share the minimal set of changes needed so people can rely on the latest version of VS Code, have a straightforward upgrade path and low maintenance effort.

## Getting started

### Docker

- Start the server:
```bash
docker run -it --init -p 3000:3000 -v "$(pwd):/home/workspace:cached" gitpod/openvscode-server
```
- Visit the URL printed in your terminal.


_Note_: Feel free to use the `nightly` tag to test the latest version, i.e. `gitpod/openvscode-server:nightly`.

#### Custom Environment
- If you want to add dependencies to this Docker image, here is a template to help:
	```Dockerfile

	FROM gitpod/openvscode-server:latest

	USER root # to get permissions to install packages and such
	RUN # the installation process for software needed
	USER openvscode-server # to restore permissions for the web interface

	```
- For additional possibilities, please consult the `Dockerfile` for OpenVSCode Server at https://github.com/gitpod-io/openvscode-releases/

#### Pre-installing VSCode extensions

You can pre-install vscode extensions in such a way:

```dockerfile
FROM gitpod/openvscode-server:latest

ENV OPENVSCODE_SERVER_ROOT="/home/.openvscode-server"
ENV OPENVSCODE="${OPENVSCODE_SERVER_ROOT}/bin/openvscode-server"

SHELL ["/bin/bash", "-c"]
RUN \
    # Direct download links to external .vsix not available on https://open-vsx.org/
    # The two links here are just used as example, they are actually available on https://open-vsx.org/
    urls=(\
        https://github.com/rust-lang/rust-analyzer/releases/download/2022-12-26/rust-analyzer-linux-x64.vsix \
        https://github.com/VSCodeVim/Vim/releases/download/v1.24.3/vim-1.24.3.vsix \
    )\
    # Create a tmp dir for downloading
    && tdir=/tmp/exts && mkdir -p "${tdir}" && cd "${tdir}" \
    # Download via wget from $urls array.
    && wget "${urls[@]}" && \
    # List the extensions in this array
    exts=(\
        # From https://open-vsx.org/ registry directly
        gitpod.gitpod-theme \
        # From filesystem, .vsix that we downloaded (using bash wildcard '*')
        "${tdir}"/* \
    )\
    # Install the $exts
    && for ext in "${exts[@]}"; do ${OPENVSCODE} --install-extension "${ext}"; done
```

### Linux

- [Download the latest release](https://github.com/gitpod-io/openvscode-server/releases/latest)
- Untar and run the server
	```bash
	tar -xzf openvscode-server-v${OPENVSCODE_SERVER_VERSION}.tar.gz
	cd openvscode-server-v${OPENVSCODE_SERVER_VERSION}
	./bin/openvscode-server # you can add arguments here, use --help to list all of the possible options
	```

  From the possible entrypoint arguments, the most notable ones are
	- `--port` - the port number to start the server on, this is 3000 by default
	- `--without-connection-token` - used by default in the docker image
	- `--connection-token` & `--connection-token-file` for securing access to the IDE, you can read more about it in [Securing access to your IDE](#securing-access-to-your-ide).
	-  `--host` - determines the host the server is listening on. It defaults to `localhost`, so for accessing remotely it's a good idea to add `--host 0.0.0.0` to your launch arguments.

- Visit the URL printed in your terminal.

_Note_: You can use [pre-releases](https://github.com/gitpod-io/openvscode-server/releases) to test nightly changes.

### Securing access to your IDE

Since OpenVSCode Server v1.64, you can access the Web UI without authentication (anyone can access the IDE using just the hostname and port), if you need some kind of basic authentication then you can start the server with `--connection-token YOUR_TOKEN`, the provided `YOUR_TOKEN` will be used and the authenticated URL will be displayed in your terminal once you start the server. You can also create a plaintext file with the desired token as its contents and provide it to the server with `--connection-token-file YOUR_SECRET_TOKEN_FILE`.

If you want to use a connection token and are working with OpenVSCode Server via [the Docker image](https://hub.docker.com/r/gitpod/openvscode-server), you will have to edit the `ENTRYPOINT` in [the Dockerfile](https://github.com/gitpod-io/openvscode-releases/blob/main/Dockerfile) or modify it with the [`entrypoint` option](https://docs.docker.com/compose/compose-file/compose-file-v3/#entrypoint) when working with `docker-compose`.

### Deployment guides

Please refer to [Guides](https://github.com/gitpod-io/openvscode-server/tree/docs/guides) to learn how to deploy OpenVSCode Server to your cloud provider of choice.

## The scope of this project

This project only adds minimal bits required to run VS Code in a server scenario. We have no intention of changing VS Code in any way or to add additional features to VS Code itself. Please report feature requests, bug fixes, etc. in the upstream repository.

> **For any feature requests, bug reports, or contributions that are not specific to running VS Code in a server context, please go to [Visual Studio Code - Open Source "OSS"](https://github.com/microsoft/vscode)**

## Documentation

All documentation is available in [the `docs` branch](https://github.com/gitpod-io/openvscode-server/tree/docs) of this project.

## Supporters

The project is supported by companies such as [GitLab](https://gitlab.com/), [VMware](https://www.vmware.com/), [Uber](https://www.uber.com/), [SAP](https://www.sap.com/), [Sourcegraph](https://sourcegraph.com/), [RStudio](https://www.rstudio.com/), [SUSE](https://rancher.com/), [Tabnine](https://www.tabnine.com/), [Render](https://render.com/) and [TypeFox](https://www.typefox.io/).

## Contributing

Thanks for your interest in contributing to the project 🙏. You can start a development environment with the following button:

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/from-referrer)

To learn about the code structure and other topics related to contributing, please refer to the [development docs](https://github.com/gitpod-io/openvscode-server/blob/docs/development.md).

## Community & Feedback

To learn what others are up to and to provide feedback, please head over to the [Discussions](https://github.com/gitpod-io/openvscode-server/discussions).

You can also follow us on Twitter [@gitpod](https://twitter.com/gitpod) or come [chat with us](https://www.gitpod.io/chat).

## Legal
This project is not affiliated with Microsoft Corporation.


### **Section 10**

#### Backend pour le panel d'administration.

- Lien du `Backend` [backend_cafe](https://github.com/Sergioanino/backend_cafe)

| Légende de fonctionnalités | Prises en charge par l'API |
| -------------------------- | -------------------------- |
| Oui                        | :white_check_mark:         |
| Non                        | :x:                        |

1. Configuration d'un `backend`.
2. Connection à [MongoDB atlas](https://www.mongodb.com/).
3. Remplir la `base de données` avec des données.

| Fonctionnalité       | Android            | iOS                | Web                | Requête & Méthode |
| -------------------- | ------------------ | ------------------ | ------------------ | ----------------- |
| Créer user           | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Actualiser user      | :white_check_mark: | :white_check_mark: | :white_check_mark: | PUT               |
| Obtenir user paginer | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Effacer user         | :white_check_mark: | :white_check_mark: | :white_check_mark: | DEL               |
| Login                | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Google login         | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Obtenir catégories   | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Créer catégorie      | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Actualiser catégorie | :white_check_mark: | :white_check_mark: | :white_check_mark: | PUT               |
| Effacer catégorie    | :white_check_mark: | :white_check_mark: | :white_check_mark: | DEL               |
| Obtenir produits     | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Obtenir produit      | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Créer produit        | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Actualiser produit   | :white_check_mark: | :white_check_mark: | :white_check_mark: | PUT               |
| Effacer produit      | :white_check_mark: | :white_check_mark: | :white_check_mark: | DEL               |
| Recherches           | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Télécharger fichier  | :white_check_mark: | :white_check_mark: | :white_check_mark: | POST              |
| Actualiser image     | :white_check_mark: | :white_check_mark: | :white_check_mark: | PUT               |
| Obtenir image Path   | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |
| Régénération Token   | :white_check_mark: | :white_check_mark: | :white_check_mark: | GET               |

---

### **Section 11**

#### Authentication et protection des routes.

- Nous allons utiliser le package **dio** pour lier notre _backend_ à notre authentification d'utilisateurs de notre site web.

---

### **Section 12**

#### Créer le UI de la view Catégorie et lier le Backend de notre API à la page web.

- Widget PaginatedDataTable,
- Pagination,
- Modals,
- CRUD,
- Prompts,
- DataTableSource.

---

### **Section 13**

#### Optimisation des routes pour éviter que notre application se redessine à tout moment.

- Changement du **navigateTo** --> `replaceTo`. [^2]

- Changement du **pushNamed** --> `pushReplacementNamed`. [^3]

[^2]: navigateTo garde les anciennes views en derrière plan.
[^3]: pushNames garde les anciennes views en derrière plan.

---

### **Section 14**

#### Gestion des utilisateurs de l'application.

- Trier le tableau par les en-têtes de colonne,
- Segments d'URL,
- Formulaire,
- Conception à deux colonnes,
- Valider le segment d'URL par rapport au backend,
- Traitement des erreurs.

---

### **Section 15**

#### Télécharger des fichiers dans le backend et le lier avec Cloudinary et Déploiement de la version de notre application sur le web avec Heroku.

- Cette section a pour but de télécharger des fichiers vers un backend à l'aide d'un sélecteur de fichiers.
- Nous allons également déployer notre backend et l'application Flutter vers un backend en ligne afin qu'il puisse être utilisé de n'importe où dans le monde. `#193 à #196`.
- Voir les étapes pour le [déploiement](https://docs.google.com/document/d/1W7xzfet0CbSPpZhR6251TDfYB1otAS0EMPZsCDP2m0Y/edit?usp=sharing) de l'application de production dans la `section 15`.

---

# Utilisation des outils suivant :

- [Visual Studio Code](https://code.visualstudio.com/)
- [Dart](https://dart.dev/)
- [Flutter](https://flutter.dev/)
- [Git](https://git-scm.com/)
- [GitHub](https://github.com/)
- [QuickType](https://quicktype.io/)
- [Node.js](https://nodejs.org/en/)
- [PostMan](https://www.postman.com/)
- [MongoDBAtlas](https://www.mongodb.com/atlas/database)
- [MongoDBCompass](https://www.mongodb.com/products/compass)
- [Cloudinary](https://cloudinary.com/)
- [Heroku](https://id.heroku.com/login)

Github : Tags

PS C:\Users\admin\Desktop\Flutter\flutter_mobile\hello-world-docker-action> git tag -a -m "My first action release" v1

PS C:\Users\admin\Desktop\Flutter\flutter_mobile\hello-world-docker-action> git push --follow-tags
