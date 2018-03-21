# SWAP 2017/2018 : PORTFOLIO DE PRÁCTICAS


##  PRÁCTICA 1: Preparación de las herramientas

* 1 -> Primero y, siguiendo los consejos del archivo pdf de la práctica 1, procedemos a la instalación de **VMware Player**.

* 2 -> Una vez descargado, pasaremos a la configuración de las 2 máquinas virtuales, en las que instalaremos el SO **Ubuntu Server 16.04.4 LTS**, el cuál obtendremos de la siguiente URL : 
https://www.ubuntu.com/download/server

		NOTA: A la hora de instalar Ubuntu Server en ambas máquinas virtuales, en mi caso, no me dejaba seleccionar más de un servicio (SSH, LAMP server, etc), por lo que elegí la opción de OpenSSH server y, una vez instalada, en el terminal, instalé el servicio LAMP, a través del siguiente comando : 
		
		$ sudo apt-get install apache2 mysql-server mysql-client	

* 3 -> Lo siguiente que he hecho ha sido activar la cuenta de **root**, con el comando : 

		$ sudo passwd root

		Y, posteriormente, le añado su clave correspondiente.

* 4 -> Después, pasamos a instalar **cURL** 

		Para ello, basta con la órden :
		$ sudo apt-get install curl

* 5 -> A continuación, pasamos a modo **root**, entramos en el directorio _/var/www/html_, y creamos el fichero _"hola.html"_ en **ubuserver01** :


		<HTML>
		<BODY>
		Archivo local en Ubuntu-Server-01. Esto funciona :)
		</BODY>
		</HTML>
___

y _"hola2.html"_ en **ubuserver02** con el siguiente cuerpo :

	<HTML>
	<BODY>
	Archivo local en Ubuntu-Server-02. Esto también funciona :D
	</BODY>
	</HTML>
	

	NOTA: Para editar desde el Terminal, he utilizado la herramienta "vim".

---	
** MODO DE USO herramienta vim **	

		$ vim hola.html
			- pulsas "i", para entrar en modo de edición
			- editas el archivo
			- pulsas escape
			- escribes :w para guardar
			- escribes :q para salir del editor en línea
---

**A continuación, hay que obtener las direcciones IP de ambas máquinas. Ésto lo haremos con la siguiente órden : `$ ifconfig`**



	
* 6 -> Ahora, nos iremos a la máquina correspondiente al servidor 2 (**Ubuntu-Server-02**) y, mediante la orden `$ ifconfig`, obtenemos la dirección IP, que es : ubuserver02 : _192.168.18.131_ . Con esto, lo que pretendemos es acceder a ella, desde la máquina uno.

Para esto, desde la máquina 1, introducimos la órden : 

		$ ssh ubuserver02@192.168.18.131
	
y, tras introducir la clave correspondiente al login ubuserver02, de la máquina 2, habríamos accedido a dicha máquina :

![ConexiónDeUbuserver01aUbuServer02](https://github.com/Jesus715/SWAP_2017-2018/blob/master/cURLde_ubuserver01aubuserver02.png) 
	 
___	 
	 
	 
ubuserver01 : 192.168.18.132
	
	