# PRÁCTICA 5: Replicación de bases de datos MySQL



* **PRIMER PUNTO : Crear una BD e insertar datos**

	-- En la máquina **ubuserver01** :
	
	Accedemos a modo **root** y entramos a la interfaz en línea de comandos de **MySQL** con : 

			$ mysql -uroot -p
			
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



___

* **SEGUNDO PUNTO : Configuración del cortafuegos**

