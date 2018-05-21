# PRÁCTICA 5: Replicación de bases de datos MySQL



* **PRIMER PUNTO : Crear una BD e insertar datos**

	-- En la máquina **ubuserver01** :
	
	Accedemos a modo **root** y entramos a la interfaz en línea de comandos de **MySQL** con : 

			$ mysql -u root -p
			
	Para entrar me pide insertar una clave. Esa clave se corresponde a la clave de _root_ de la máquina _ubuserver01_. Tras esto, ya estaremos dentro del monitor de MySQL.

	Ahora, vamos a crear nuestra primera base de datos, `contactos`y usarla para introducirle datos :
	
			mysql> create database contactos;
			mysql> use contactos;
			
			Con el comando:
			mysql> show tables;
			vemos todas las tablas que hayamos creado en la BD.
			Ahora nos aparecera vacía.
			
			Dentro de contactos, voy a crear la primera tabla, a la que voy a llamar 'datos'. Y le especifico cuántas columnas va a tener dicha tabla, y qué tipo de datos van a corresponder a cada columna : 
			
		mysql> create table datos (nombre varchar(100), tlf int)

			Lo siguiente es insertarle los datos que queramos a la tabla. Esto se hace mediante la siguiente línea : 
		
		mysql> insert into datos (nombre,tlf) values ("Jesus", 958596528);
		
			*Haremos más de dos inserciones.

			Y con el comando:
			mysql> select * from datos;
			Estamos diciendo que nos muestre todo(*) de la tabla datos.
			
	Nuestra tabla en la máquina **ubuserver01** quedaría así :

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P5/tablaDATOSubuserver01.png) 

Y salimos de la interfaz de comandos en línea.


___

* **SEGUNDO PUNTO : Realizar una copia de seguridad con mysqldump**

Antes de hacer la copia de seguridad en el archivo .sql debemos evitar que se acceda a la BD para cambiar nada, bloqueando las tablas.

Para ello, de nuevo en la máquina **ubuserver01**, entramos en **root**, y accedemos al monitor mysql. 

		Una vez dentro del monitor de comandos :
		mysql> FLUSH TABLES WITH READ LOCK;
		Y salimos : 
		mysql> quit
		
Ahora ya sí podemos hacer el _mysqldump_ para guardar los datos. En el servidor principal (**ubuserver01**) hacemos :

		$ mysqldump contactos -u root -p > /tmp/contactos.sql

Como habíamos bloqueado las tablas, debemos desbloquearlas (quitar el “LOCK”):

		$ mysql -uroot -p
		introducimos la clave de root de ubuserver01
		
		mysql> UNLOCK TABLES;
		mysql> quit
		
Ahora, vamos a irnos a la máquina **ubuserver02**, la cuál usaremos como esclavo, vamos a entrar al modo **root**, y vamos a coger el fichero `contactos.sql`guardado en _/tmp/_ en la máquina1 :

		$ scp 192.168.18.132:/tmp/contactos.sql /tmp/
		
Aquí vemos cómo se ha realizado correctamente la copia : 

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P5/scpDEubuserver1Enubuserver2.png) 

Ahora, en la **máquina 2**, vamos a entrar en la interfaz de comandos en línea de **MySQL** y vamos a crear la BD vacía a la que le vamos a pasar la copia de la que tenemos en la máquina _ubuserver01_ :

		$ mysql -u root -p
		Introducimos la clave correspondiente a ubuserver02
		
		mysql> create database contactos;
		mysql> quit
		
Como vemos, hemos creado una BD vacía en **ubuserver02** :

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P5/CONTACTOSdeUbu2AntesDEcopiar.png) 

A continuación vamos a volcar el contenido del fichero `contactos.sql` que nos hemos traído desde **ubuserver01**, en fichero vacío de contactos en la BD de **ubuserver02** :

		$ mysql -u root -p contactos < /tmp/contactos.sql