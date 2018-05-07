# PRÁCTICA 4: Asegurar la granja web


* **PRIMER PUNTO : Crear e instalar en la máquina 1 un certificado SSL autofirmado**


En primer lugar accederé al modo **root**, para poder ejecutar las siguientes líneas de comando : 

		$ a2enmod ssl
		$ service apache2 restart
		$ mkdir /etc/apache2/ssl
		
Tras ejecutar la siguiente orden :
`$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt`

Tendremos que indicar una serie de datos que se nos pedirán. Los introducimos para que queden de la siguiente manera : 
