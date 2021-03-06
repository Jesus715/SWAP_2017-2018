##  PRÁCTICA 2: Clonar la información de un sitio web

 * **PRIMER PUNTO : funcionamiento de la copia de archivos por ssh** 
 Tanto en la máquina1, como en la 2, voy a ponerme en modo _**root**_, y voy a darle permisos de lectura y escritura (644) al archivo **sshd_config** que se encuentra en el directorio _/etc/ssh_ de cada máquina.
 Abrimos el fichero con la herramienta **vim**, presentada en la práctica anterior, y modificamos el apartado 
 
 		PermitRootLogin prohibit-password 
 para que quede de la siguiente forma :
 		
 		PermitRootLogin yes
 salimos del modo de edición(ESC), guardamos (:w), y salimos del editor (:q). Para finalizar la configuración de ssh, reiniciamos con la órden :
 
 		$ sudo service ssh restart
 
	Tras esto, lo único que hay que hacer es lo siguiente : 
![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/tarde1a2.png) 
![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/tarde2a1.png) 
	
* **SEGUNDO PUNTO : clonado de una carpeta entre las dos máquinas** 

De nuevo, y en ambas máquinas, me voy a poner en modo **root** y voy a instalar el paquete _**rsync**_ :

	$ sudo apt-get install rsync 
	
Tras la instalación (en mi caso ya estaba hecha), salimos del modo root.

Lo siguiente es hacer que el usuario sea el dueño de la carpeta donde residen los archivos que hay en el espacio web, para no tener que entrar en el modo **root** (en ambas máquinas):

	$ sudo chown ubuserver0X:ubuserver0X –R /var/www

Para probar el funcionamiento del rsync, vamos a clonar la carpeta con el contenido del servidor web principal de la máquina 2, en la máquina 1 (y viceversa en la máquina 2 con el contenido de la máquina 1). Esto lo haremos con la órden :

$ rsync -avz -e ssh ubuserver02@192.168.18.131:/var/www/ /var/www/

y tras meter la clave correspondiente al usuario "ubuserver02" de la máquina 2, ya estaría hecho.

Aquí vemos el estado del directorio _/var/www/html/_ antes de hacer **rsync** : 

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/antesdeRSYNCenubu1.png) 

Como vemos, se han copiado los archivos `hola2.html`,`index.html` y `pruebacrontab.txt`, correspondientes a la máquina 2 :

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/despuesDersyncEnubu1.png) 

De la misma manera actuaríamos para la máquina 2 :

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/antesdeRSYNCenubu2.png) 

Y así es como quedaría el directorio _/var/www/html/_ tras el **rsync**, en la máquina 2 : 

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/despuesDersyncEnubu2.png) 

* **TERCER PUNTO : Acceso sin contraseña para ssh** 
			
Dentro de ubuserver01 :
 
			1.  $ ssh-keygen -b 4096 -t rsa
			2.  $ ssh-copy-id ubuserver02@192.168.18.131

Y ya estaría listo.

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/sshde1a2.png) 

De forma análoga haríamos para sincronizar desde la máquina 2 :

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/sshde2a1.png) 

* **CUARTO PUNTO : Programar tareas con crontab** 
Vamos a _/etc/_ y abrimos con vim el fichero **crontab**.
En el editor en línea programamos para que se actualice el contenido de _/var/www/_ correspondiente a la máquina 2 en la máquina 1, cada hora (en mi caso, lo he programado para que se haga a las y 15). 
Esto se hace de la siguiente manera : 

15 *		* * *	root		rsync -avz -e ssh ubuserver02@192.168.18.131:/var/www/ /var/www/
	
Así quedaría el archivo crontab de mi máquina 1 :

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/crontab.png) 

Para probar que se realiza correctamente, he creado un fichero de prueba en el directorio _/var/www/_ de la máquina 2, llamado _pruebacrontab.txt_. Este fichero deberá de aparecer en el directorio de la máquina 1, cuando haya pasado 1h y se haya ejecutado la órden del crontab. 

- Aquí tenemos la vista local en la máquina 2 : 
![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/antesdeCRONTABubu2.png) 

- Aquí tenemos la vista local en la máquina 1, antes de la ejecución del crontab (a la espera de que den las 0X:15): 
![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/antesdeCRONTABubu1.png) 

- Y, por último, en la siguiente imágen, de forma local en la máquina 1, vemos que se ha ejecutado correctamente el crontab y ha clonado los archivos en la máquina 1 a las y 15:

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P2/despuesDEcrontabUbu1.png) 


 


