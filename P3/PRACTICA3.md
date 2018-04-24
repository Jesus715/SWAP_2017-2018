#PRÁCTICA 3: Balanceo de carga

Lo primero que he tenido que hacer es cambiar el idioma del terminal, ya que, por defecto, me venía en inglés. 
Para ello, he entrado en modo **_root_** y he introducido el siguiente comando : 

		$ loadkeys es
		
donde `es` hace referencia al idioma seleccionado : español

Me voy a mantener como **_root_**, porque lo voy a necesitar a continuación.

* **PRIMER PUNTO : configurar una máquina e instalar el nginx como balanceador de carga**


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

	