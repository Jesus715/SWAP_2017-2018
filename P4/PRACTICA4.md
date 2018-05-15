# PRÁCTICA 4: Asegurar la granja web


* **PRIMER PUNTO : Crear e instalar en la máquina 1 un certificado SSL autofirmado**


En primer lugar accederé al modo **root**, para poder ejecutar las siguientes líneas de comando : 

		$ a2enmod ssl
		$ service apache2 restart
		$ mkdir /etc/apache2/ssl
		
Tras ejecutar la siguiente orden :
`$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt`

Tendremos que indicar una serie de datos que se nos pedirán. Los introducimos para que queden de la siguiente manera : 

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P4/instalacionSSL.png) 

A continuación, vamos a editar el archivo de configuración `default-ssl.conf` con **nano** :

`$ sudo nano /etc/apache2/sites-available/default-ssl.conf`


Nos	queda de la siguiente manera :

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P4/defaultSSLconfModificado.png) 

Ahora, activamos el sitio default-ssl y reiniciamos apache con:

		$ a2ensite default-ssl
		$ service apache2 reload

Para que la otra máquina y el Balanceador tengan el certificado, hago un `rsync` de la máquina donde generé el certificado **ubuserver01**, desde la máquina que quiero recibir el directorio :


Desde ubuserver02 :
**entro en modo root primero**, y ejecuto :
`$ rsync -avz -e ssh ubuserver01@192.168.18.132:/etc/apache2/ssl /etc/nginx/` 

Seguidamente, tenemos que modificar el fichero `default-ssl.conf`, y dejarlo de la misma forma que hicimos anteriormente con el de la máquina1, con la siguiente diferencia : 

			SSLCertificateFile /etc/nginx/ssl/apache.crt
			SSLCertificateKeyFile /etc/nginx/ssl/apache.key

Para la máquina balanceadora seguiré este mismo proceso de configuración y, además, modificaré el archivo `default.conf`para que quede de la siguiente manera : 

**Comento ssl on para que funcione correctamente.**

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P4/defaultSSL.png) 

Tras esto, ya podemos comprobar cómo haciendo un **curl** en mi PC local, tanto con _http_, como con _https_, nos devuelve los `index.html` correspondientes : 

-- **HTTP :**
![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P4/curlHTTP.png) 

-- **HTTPS :**
![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P4/curlHTTPS.png) 

___

* **SEGUNDO PUNTO : Configuración del cortafuegos**

Esta configuración la he hecho en el **Balanceador**. La definición de todas las reglas las he hecho en un script en el archivo `/etc/rc.local`.

Lo primero que he hecho es copiar y renombrar el archivo `rc.local` con el nombre `rc.local.backup` : 

		$ sudo cp rc.local rc.local.backup

Despues, defino reglas para permitir acceso por la interfaz, apertura del puerto 22 (ssh), puerto 80 y 443 (para HTTP y HTTPS).
La interfaz de mi máquina balanceadora es **ens33**.


