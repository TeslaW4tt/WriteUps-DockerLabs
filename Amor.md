# Escaneo


Realizamos un escaneo con nmap

`nmap -sVC -p- -n -Pn  --min-rate 5000 172.17.0.2-oN escaneo` 

![Escaneo de puertos](Imagenes/amor/1.PNG)

Observamos que tenemos el puerto 80 y el puerto 22 abiertos, por lo que en el navegador web colocamos la dirección IP de la maquina victima.

![Escaneo de puertos](Imagenes/amor/2.PNG)

Encontramos 2 posibles usuarios *carlota* y *juan*.
Utilizando *hydra* realizamos una ataque de fuerza bruta para encontrar la posible contraseña del usuario carlota 

![Escaneo de puertos](Imagenes/amor/3.PNG)

Encontramos la password asi que nos logeamos utilizando el puerto 22 ssh.

![Escaneo de puertos](Imagenes/amor/4.PNG)

Una vez dentro de la maquina podemos ver que existen 3 usuarios por lo que tenemos que hacer el pivoting 

![Escaneo de puertos](Imagenes/amor/5.PNG)

Dentro del directorio de carlota encontramos una *iagen-jpg* por lo que para poderla analizar creamos un servidor en python 

![Escaneo de puertos](Imagenes/amor/6.PNG)
En nuestra maquina atacante obtenemos la imagen de la maquina victima 

![Escaneo de puertos](Imagenes/amor/7.PNG)

Con la herramienta *steghide* extraemos la información que podría estar encriptada dentro de la imagen.

![Escaneo de puertos](Imagenes/amor/8.PNG)

Obtenemos un archivo *secreto.txt* asi que lo leemos con cat y vemos que tiene un hash

![Escaneo de puertos](Imagenes/amor/9.PNG)

Utilizando una web para desencriptar encontramos lo que podría ser la contraseña del usuario *oscar*

![Escaneo de puertos](Imagenes/amor/10.PNG)

Accedemos como usuario oscar.

![Escaneo de puertos](Imagenes/amor/11.PNG)

Ejecutamos el comando *sudo -l* para encontrar que binarios podemos ejecutar como usuario root

![Escaneo de puertos](Imagenes/amor/12.PNG)


En la pagina de GTObins buscamos el binario de ruby 

![Escaneo de puertos](Imagenes/amor/13.PNG)

Ejecutamos el binario y somos root.

![Escaneo de puertos](Imagenes/amor/14.PNG)


 #                                P W N E D !



