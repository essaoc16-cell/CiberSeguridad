Inicializamos la máquina PapaFrita y Kali Linux 
![[Pasted image 20260929220059.png]]
![[Pasted image 20260929220153.png]]

En Kali, abrimos la terminal y ejecutamos el comando, sudo su.
Procedemos a hacer el reconocimiento de vulnerabilidades de PapaFrita con Nmap.
usamos el siguiente comando: nmap -sV -sC 192.168.1.6

![[Pasted image 20260929231217.png]]


Tomamos en cuenta que tenemos un puerto 22 y 80. Ahora verificamos la página web con la ip.
![[Pasted image 20260929221554.png]]

Verificamos si en el código fuente de la página encontramos algo que nos pueda ayudar.
Click derecho -> view page source
![[Pasted image 20260929232322.png]]

Encontramos algo interesante, así que vamos a revisar de que se trata.

![[Captura de pantalla 2026-09-29 232636.png]]


Nos dice que es código Brainfuck, para decifrarlo vamos a https://www.dcode.fr/brainfuck-language 

![[Pasted image 20260929233115.png]]


Vamos a pensar que sea una contraseña, la que hemos encontrado abuelitacalientalasopa, entonces nos faltaría un usuario, vamos a hacer un ataque te fuerza bruta con la herramienta hydra.
hydra -L /usr/share/wordlists/rockyou.txt -p abuelacalientalasopa ssh://192.168.1.6
![[Pasted image 20260930004217.png]]
Intentamos con palabras del password y observamos que con `abuela` podemos acceder.
![[Pasted image 20260930004358.png]]
Se ha encontrado el usuario y contraseña
Realizamos un sudo -l  y podemos ver se puede elevar privilegios haciendo uso del binario `node` podemos acceder como root.
![[Pasted image 20260930004612.png]]

Vamos a la  plataforma https://gtfobins.org/, para tener el código según el bin
![[Pasted image 20260930004832.png]]

Y así conseguimos el acceso root.
![[Pasted image 20260930005117.png]]

