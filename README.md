# Proyecto 2 - T贸picos especiales en Telem谩tica 馃摱

En este documento se explicar谩 con detalle t茅cnico y de instalaci贸n el desarrollo de este proyecto, as铆 como los pasos para instalarse y poder replicar nuestros resultados.

Este proyecto fue desarrollado en GCP con algunas de sus herramientas por lo que los nombres har谩n referencias a configuraciones de esta plataforma, pero puede hacerse lo mismo en otras IaaS.

## Dise帽o l贸gico de la implementaci贸n
![A](https://user-images.githubusercontent.com/53051441/140453547-66ec9f20-d62e-4872-86a0-adf11138c40c.png)

## Configuraci贸n e inicializaci贸n de instancias

<p align="center"><img width="300px" src="https://user-images.githubusercontent.com/52968530/138364996-75e63672-050f-453d-999f-475aaf4b5547.png" /></p>

Utilizando el Compute Engine de GCP, montamos las instancias de VM para nuestra infraestructura. Las VM implementadas son los `main` servers, los `gallery` servers y los `load-balancer` servers.

En la siguiente tabla se resumen las configuraciones iniciales:

|**Servidor**|**Configuraci贸n**|
|-----|-----|
|`load-balancer`|![image](https://user-images.githubusercontent.com/52968530/139148172-d2d79966-0ad8-4bd9-9c5f-b7ec0fe5e426.png)<br/>![image](https://user-images.githubusercontent.com/52968530/139148409-082557b9-1a36-4a9c-beb0-dfebabb4feb1.png)<br/>![image](https://user-images.githubusercontent.com/52968530/139148508-2afd49ea-a75d-4d39-861b-8915f1b7a840.png)|
|`main` y `gallery`|![image](https://user-images.githubusercontent.com/52968530/139148172-d2d79966-0ad8-4bd9-9c5f-b7ec0fe5e426.png)<br/>![image](https://user-images.githubusercontent.com/52968530/139148409-082557b9-1a36-4a9c-beb0-dfebabb4feb1.png)<br/>![image](https://user-images.githubusercontent.com/52968530/139148892-b6934608-97d7-444e-beda-17515223b156.png)|

Cada m谩quina se configur贸 con los siguientes comandos:
```
# Updating system
sudo apt update -y && sudo apt upgrade -y
sudo apt install wget -y
sudo apt install git -y

# Installing docker and docker-compose 
sudo wget -O - https://bit.ly/docker-install | bash

# Downloading the project
git clone https://github.com/juansedo/tet-challenge2.git
```

## Configuraci贸n de DNS
<p align="center"><img width="300px" src="https://user-images.githubusercontent.com/52968530/138371468-5d345846-7aa0-4fff-a884-a691c46493ae.png" /></p>

Ya que tenemos las IP p煤blicas de las m谩quinas, con el servicio de Freenom se puede solicitar un dominio gratuito. La configuraci贸n del DNS queda as铆:

![image](https://user-images.githubusercontent.com/52968530/139149976-b13fffca-8ee5-46ed-98e4-0dd2e00426b6.png)

## Inicio de los servidores

Aqu铆 se diferencian los dos servidores que se tienen en el mismo repositorio. Por lo que se puede ejecutar uno u otro:

```
# Starting main
cd tet-challenge2/wordpress/
cp .env.example .env
sudo docker-compose up -d

# Starting gallery
cd tet-challenge2/wordpress/
cp .env.example2 .env
sudo docker-compose up -d

# Starting load balancer for main
cd tet-challenge2/load-balancer/lb-main
cp .env.example .env
sudo nano nginx/nginx.conf # Check and update upstream ip's
sudo docker-compose up -d
```

### `main`

Este servidor contiene la p谩gina inicial del proyecto con un feed donde se pueden visualizar los proyectos de P1 y P2. La parte visual se realiz贸 de forma manual manteniendo el volumen `wordpress` con esta informaci贸n.

### `gallery`

Este servidor contiene una galer铆a de distribuci贸n aleatoria de los proyectos de P1 y P2. La parte visual se realiz贸 de forma manual manteniendo el volumen `wordpress` con esta informaci贸n.

### `load balancer`

Este servidor despliega un contenedor `nginx` con la configuraci贸n necesaria para tener un balanceador de carga. Dado que el archivo `nginx` no se puede controlar con variables de entorno de forma simple, se cre贸 la configuraci贸n espec铆fica de cada balanceador (uno por p谩gina) y por esto dos carpetas.


## Content Delivery Network (CDN)
<p align="center"><img width="300px" src="https://mma.prnewswire.com/media/1344798/CDN_net_Logo.jpg?p=twitter" /></p>
Utilizamos la prueba gratuita de 14 d铆as de cdn.net, la cu谩l decidimos solo implementar en la p谩gina principal y en un subdominio para simplificar la presentaci贸n de lo que se ha implementado.

As铆, la ruta http://cdn.proyecto2-tet.tk es el proyecto gestionado por un CDN.

## Reportes `uptime` del servidor
<p align="center"><img width="300px" src="https://user-images.githubusercontent.com/52968530/140233371-f9554009-49dc-434e-8ad4-15fddbe719da.png" /></p>

Para generar estos reportes escogimos una cuenta gratuita de Site24x7 que permite generar reportes de estado de salud de los servicios, monitorear sus certificados, verificar tiempos de carga e incluso analizar servicios o m谩quinas VM de nubes espec铆ficas (GCP, AWS, etc). Incluye notificaciones al correo de cambios de estado.
<p align="center"><img width="400px" src="https://user-images.githubusercontent.com/52968530/140232892-865fffa9-4537-4df2-82f1-9fd4ec15cb10.png" /></p>


## Plugins de Wordpress

En Wordpress se hicieron configuraciones adicionales correspondientes a la instalaci贸n de plugins que permitieran configuraciones adicionales como el *Single Sign On* y el *Two Factor Authentication*. Mencionaremos los instalados y una gu铆a oficial que utilizamos para la configuraci贸n de los servicios:

### Single Sign On
<img width="200px" src="https://www.drupal.org/files/project-images/brand%20evolution_logo_Auth0_black.png" alt="auth0-logo">
Configuraci贸n hecha con Auth0 y ampliamente guiada por esta gu铆a:
https://auth0.com/blog/wordpress-sso-with-auth0/

### Two Factor Authentication
<img width="200px" src="https://www.drupal.org/files/project-images/brand%20evolution_logo_Auth0_black.png" alt="auth0-logo">
Configuraci贸n hecha con Auth0 y ampliamente guiada por esta gu铆a:
https://auth0.com/docs/login/mfa/mfa-factors/configure-sms-voice-notifications-mfa

### Database and Page Cache (NO FUNCION脫 EN LA IMPLEMENTACI脫N)
<img width="200px" src="https://onlinezebra.com/wp-content/uploads/2021/03/w3-total-cache-logo.png" alt="w3tc-logo">
<img width="200px" src="https://yosoy.dev/wp-content/uploads/2017/12/Redis_Logo.png" alt="redis-logo">
Configuraci贸n hecha con W3 Total Cache y Redis
https://thibaut-deveraux.medium.com/a-docker-compose-file-to-install-wordpress-with-a-traefik-reverse-proxy-an-ssl-certificate-and-a-e878c2a03a17


## Participantes 馃毠

|Nombre||
|------|-------|
|David Calle Gonz谩lez|<a href="https://github.com/dcalleg707"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/calle_dcg"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
|Juan Sebasti谩n D铆az Osorio|<a href="https://github.com/juansedo"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/juansedo"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
|Santiago Hidalgo Ocampo|<a href="https://github.com/sanhidalgoo"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/sanhidalgoo"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
