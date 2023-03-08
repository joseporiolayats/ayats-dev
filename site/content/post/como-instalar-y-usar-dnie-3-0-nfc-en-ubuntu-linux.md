---
title: Como instalar y usar DNIe 3.0 NFC en Ubuntu linux
date: 2023-03-08T18:17:24.828Z
description: Guia practica para instalar, usar y sobrevivir con el certificado
  digital del DNIe 3.0 en linux, Ubuntu 22.10 (2023)
---
R﻿equisitos previos

I﻿nstalar openjdk

```
s﻿udo snap install openjdk
```



Instalar libssl1.1 , es una libreria antigua.

```
echo "deb http://security.ubuntu.com/ubuntu focal-security main" | sudo tee /etc/apt/sources.list.d/focal-security.list
sudo apt update
sudo apt install libssl1.1
dpkg -L libssl1.1
```

D﻿escargar la aplicacion DNIeRemoteWizard
I﻿r a la sede DNI Electronico www.dnielectronico.es y en el menu de la izquierda "Area de Descargas" clicar y buscar la aplicacion de linux 64bit,
o﻿ directamente hacer click [aqui](https://www.dnielectronico.es/portaldnie/PRF1_Cons02.action?pag=REF_1015&id_menu=65)
