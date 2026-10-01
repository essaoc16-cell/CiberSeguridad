Primero abrimos la terminal de Kali Linux
<img width="1917" height="1091" alt="image" src="https://github.com/user-attachments/assets/f56c2258-2634-4d14-b7cc-9c07adeb2dc9" />

![[Pasted image 20260928215119.png]]

Scaneamos el puerto con nmap 
![[Pasted image 20260928221146.png]]

A continuación se revisa la página web que tenemos en el puerto 80
![[Pasted image 20260928225006.png]]

Ahora se realiza la enumeración de directorios y archivos utilizando Gobuster, así podemos descubrir rutas ocultas.

![[Pasted image 20260928230244.png]]

Hemos identificado una página de WordPress
![[Pasted image 20260928230655.png]]

Como Mi web No Hackeable, nos redirige a un dominio academy.thl, lo registramos en el /etc/hosts y recargamos la página.
![[Captura de pantalla 2026-09-29 000620.png]]
![[Captura de pantalla 2026-09-28 235815.png]]


Realizamos la enumeración de Fuerza Bruta con la herramienta wpscan
wpscan --url http://academy.thl/wordpress -e u p
![[Pasted image 20260929001917.png]]

Identificamos un Usuario 
![[Pasted image 20260929002120.png]]

Ahora tenemos que descubrir la contraseña
wpscan --url http://academy.thl/wordpress/ -e u --passwords  /usr/share/wordlists/rockyou.txt
![[Pasted image 20260929002937.png]]

Una vez obtenida la contraseña, nos vamos a WordPress
![[Pasted image 20260929003446.png]]

Vemos que ya tenemos acceso de administrador, revisamos los plugins, tenemos a Bill File Manager que nos permite subir archivos y directorios.
![[Pasted image 20260929003628.png]]

Creamos un archivo malicioso en reverse shell generator 
![[Pasted image 20260929005010.png]]
![[Pasted image 20260929004943.png]]
![[Pasted image 20260929005044.png]]

Y observamos la netcap
![[Pasted image 20260929010610.png]]
![[Pasted image 20260929010336.png]]

Haremos una shell interactiva para que no se nos caiga la sesión 
![[Pasted image 20260929012104.png]]

Ya teniendo acceso a la máquina víctima, descargamos de github lo que nos ayudará a analizar vulnerabilidades.
![[Pasted image 20260929012903.png]]

Y finalmente tenemos acceso a root.
![[Pasted image 20260929022950.png]]
