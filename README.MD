

#Docker-compose.yml

Descripciones de las opciones del docker-compose.yml:

version

services
    bind
        image
        ports
        volumes

volumes
    nombresvolumen

version:Colocamos la version de docker-compose que necesitemos
    services: Aqui meteremos todas las opciones
     nombre: Aqui ponemos el nombre
        image: Aqui ponemos la imagen que vamos a usar
        ports: Aqui ponemos los puertos que vamos a usar
        volumes: Aqui ponemos nuestros volumenes y las rutas necesarias para la imagen
        networks:Aqui se pondria la red externa, mas una ip estatica.
     
     nombre del cliente:
        image: Aqui ponemos la imagen que vamos a usar
        ports: Aqui ponemos los puertos que vamos a usar
        volumes: Aqui ponemos nuestros volumenes y las rutas necesarias para la imagen
        networks:Aqui se pondria la red externa, mas una ip estatica.
    volumes: Aqui creamos nuestros volumes
    conf:
 networks:La direccion de red externa.
    br02: nombre de la direccion
    external:true red externa.
    
    
    Estos ajustes serian del volumen del contenedor:
    
    Configuracion de la Zona DNS:
      sudo apt install bind9: Instalacion de bind9.
      /etc/bind/named.conf.options: para poner una direccion ip del DNS:
      forwarders {
         8.8.8.8;
         4.4.4.4;
        };
      
    /etc/bind/named.conf.local:Configuracion de la zona del nombre.
    zone "baram27.com" {
       type master;
       file "/etc/bind/db.baram27.com";
        };
        
  
  Este seria el contenedor del servidor:
  sudo cp /etc/bind/db.local /etc/bind/db.example.com:Por defecto viene otros red ip, y nombre, habrá que configurar el nombre la IP y el CNAME.
 
 ;

; BIND data file for local loopback interface ; $TTL 604800 @ IN SOA baram27.com. root.baram27.com. ( 2 ; Serial 604800 ; Refresh 86400 ; Retry 2419200 ; Expire 604800 ) ; Negative Cache TTL ; @ IN NS baram27.com. @ IN A 10.1.0.2 @ IN AAAA ::1 ns IN A 10.1.0.2

p

En el cliente: sudo apt install dnsutils:Instalo dnsutils.

root@ec754e55b1fd:/# dig baram27.com :Hago una comprobacion con el comando dig si funciona la zona creada llamada baram27.

; <<>> DiG 9.16.1-Ubuntu <<>> baram27.com ;; global options: +cmd ;; Got answer: ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 53547 ;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION: ; EDNS: version: 0, flags:; udp: 65494 ;; QUESTION SECTION: ;baram27.com. IN A

;; Query time: 48 msec ;; SERVER: 127.0.0.11#53(127.0.0.11) ;; WHEN: Wed Dec 15 16:34:58 CET 2021 ;; MSG SIZE rcvd: 40
