# PRÁCTICA 3: Balanceo de carga


* **PRIMER PUNTO : configurar una máquina e instalar el nginx como balanceador de carga**

	Lo primero que he tenido que hacer es añadir una nueva máquina virtual a la que llamo Balanceador, **sin instalarle apache, ni LAMP**.
																																																																																																																																																																						
	Después, y una vez dentro de la máquina balanceadora, he tenido que cambiar el idioma del terminal, ya que, por defecto, me venía en inglés. 
Para ello, he entrado en modo **_root_** y he introducido el siguiente comando : 

		$ loadkeys es

		
	donde `es` hace referencia al idioma seleccionado : español

	Me voy a mantener como **_root_**, porque lo voy a necesitar a continuación.



Introduzco las siguientes órdenes para la instalación de **nginx** :

		$ sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove
		$ sudo apt-get install nginx
		$ sudo systemctl start nginx

Tras esto, mi archivo de configuración no existe. Por tanto, lo creo en _/etc/nginx/conf.d/defaul.conf_ y lo configuro, con la herramienta _vim_, para que quede de la siguiente manera : 

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P3/defaultconf_nginx.png) 

Una vez hecho esto, introduzco la siguiente línea en el Terminal : 

		$ sudo systemctl start nginx
		
Me daba error y no se iniciaba **nginx**. Para solucionarlo, he tenido que modificar el archivo _/etc/nginx/nginx.conf_, comentando la siguiente línea : 

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P3/nginxconfcomentada.png) 
	
Para finalizar, reinicio nginx en el Terminal :

		$ sudo systemctl restart nginx

Y ya estaría lista la instalación y configuración de **nginx**.

Para que se nos muestre cada vez una máquina, le he dado valores distintos a la prioridad de cada una (si no especifico nada, tendrían la misma prioridad ambas). Esto se hace modificando el archivo de configuración de **nginx** para que quede de la siguiente manera : 

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P3/defaultnginxPESOS.png) 

Por último, y para comprobar el correcto funcionamiento, obtengo la dirección IP del Balanceador (192.168.18.133). 
Despues, hago un `cat` a los archivos `index.html` de cada máquina de forma local : 

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P3/ubuserver01-index.png) 
![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P3/ubuserver02-index.png) 

Ahora veremos como, llamando a curL con  la IP del **Balanceador Nginx** desde mi PC, éste nos devuelve el fichero `index.html` correspondiente, cada vez que lo llamemos, a una máquina diferente :

![](https://github.com/Jesus715/SWAP_2017-2018/blob/master/P3/curl-al-BalanceadorNginx.png)  


* **SEGUNDO PUNTO : configurar una máquina e instalar el haproxy como balanceador de carga**

	Lo primero que he tenido que hacer es añadir una nueva máquina virtual a la que llamo BalanceadorHAProxy, **sin instalarle apache, ni LAMP**.
																																																																																																																																																																						
	Después, y una vez dentro de la máquina balanceadora, he tenido que cambiar el idioma del terminal, ya que, por defecto, me venía en inglés. 
Para ello, he entrado en modo **_root_** y he introducido el siguiente comando : 

		$ loadkeys es

		
	donde `es` hace referencia al idioma seleccionado : español

	Me voy a mantener como **_root_**, porque lo voy a necesitar a continuación.

Introduzco las siguientes órdenes para la instalación de **haproxy** :
	