---
title: Como instalar y usar certificado digital DNIe 3.0 NFC en Ubuntu linux
  (DNI Electronico)
date: 2023-03-25T09:14:18.585Z
description: Guia practica para instalar, usar y sobrevivir con el certificado
  digital del DNIe 3.0 (DNI electronico NFC) en linux, Ubuntu 22.10 (2023)
image: img/dni.jpeg
---
## R﻿equisitos previos

Primero de todo es imprescindible trabajar con los ultimos paquetes de sistema y con las listas actualizadas. Asi que hay que actualizar las listas con *apt update* y luego aplicar las actualizaciones con *apt upgrade* . 

Algunos de los paquetes, probablemente Firefox, estan manejados por la Snap store, asi que tambien hay que actualizarla, a traves de *snap refresh* .

```
sudo apt update
sudo apt upgrade
sudo snap refresh
```

# Pasos necesarios:

1. Openjdk
2. Dependencias varias
3. Libreria libssl1.1
4. DNIeRemoteWizard
5. Limpiar perfil de Firefox

## 1. OpenJDK

La aplicacion de DNIe funciona con Java, asi que hay que instalar el interpretador.

```
sudo snap install openjdk
```

## 2. Dependencias varias

Algunas de las funcionalidades requieren de dependencias cruzadas que no se instalan sin hacerlo especificamente, en este caso **libnss3**

```
sudo apt install libnss3-tools
```

## 3. LibSSL1.1

Este paso es critico y hay que hacerlo segun el codigo siguiente, ya que DNIe solo funciona con la version antigua de libssl1.1, y no se instalara si no se especifica exactamente.

```
echo "deb http://security.ubuntu.com/ubuntu focal-security main" | sudo tee /etc/apt/sources.list.d/focal-security.list
sudo apt update
sudo apt install libssl1.1
dpkg -L libssl1.1
```

## 4. DNIeRemoteWizard

La aplicacion especifica para trabajar con DNIe es DNIeRemoteWizard. 

![Aplicacion para vincular DNIe al sistema](img/dnieremotewizard.png "DNIe Remote Wizard")

Para descargarla i﻿r a la sede [DNI Electronico](www.dnielectronico.es) www.dnielectronico.es y en el menu de la izquierda "Area de Descargas" clicar y buscar la aplicacion de linux 64bit,
o﻿ directamente hacer click [aqui](https://www.dnielectronico.es/portaldnie/PRF1_Cons02.action?pag=REF_1015&id_menu=65)

## 5. Limpiar perfiles en Firefox

La aplicacion especifica para trabajar con DNIe es Firefox, aunque tambien funciona en navegadores Chrome, Chromium, Opera, Brave.

Para trabajar en Firefox, hay que borrar uno de los perfiles que se instala por defecto. Para ello debemos arrancar Firefox desde la consola de comandos a traves de:

```
firefox -p
```

Aparecera un dialogo para administrar los perfiles.

E﻿liminar todos los perfiles que no sean los que acaban en *\-release* y luego *Iniciar Firefox*.

![Ventana de administracion de perfiles de Firefox para eliminar los sobrantes](img/administrador-de-perfiles.png "Administrador de perfiles de Firefox")