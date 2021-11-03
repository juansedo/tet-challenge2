# Proyecto 2 - Tópicos especiales en Telemática 📶

En este documento se explicará con detalle técnico el desarrollo de este proyecto, así como los pasos para instalarse y poder replicar nuestros resultados.

Este proyecto fue desarrollado en GCP con algunas de sus herramientas por lo que los nombres harán referencias a configuraciones de esta plataforma, pero puede hacerse lo mismo en otras IaaS.

## Diseño lógico de la implementación
...

## Diseño técnico de la implementación
...

## Configuración e inicialización de instancias

<p align="center"><img width="300px" src="https://user-images.githubusercontent.com/52968530/138364996-75e63672-050f-453d-999f-475aaf4b5547.png" /></p>

Utilizando el Compute Engine de GCP, montamos las instancias de VM para nuestra infraestructura. Las VM implementadas son los `main` servers, los `gallery` servers y los `load-balancer` servers.

En la siguiente tabla se resumen las configuraciones iniciales:

|**Servidor**|**Configuración**|
|-----|-----|
|`load-balancer`|![image](https://user-images.githubusercontent.com/52968530/139148172-d2d79966-0ad8-4bd9-9c5f-b7ec0fe5e426.png)<br/>![image](https://user-images.githubusercontent.com/52968530/139148409-082557b9-1a36-4a9c-beb0-dfebabb4feb1.png)<br/>![image](https://user-images.githubusercontent.com/52968530/139148508-2afd49ea-a75d-4d39-861b-8915f1b7a840.png)|
|`main` y `gallery`|![image](https://user-images.githubusercontent.com/52968530/139148172-d2d79966-0ad8-4bd9-9c5f-b7ec0fe5e426.png)<br/>![image](https://user-images.githubusercontent.com/52968530/139148409-082557b9-1a36-4a9c-beb0-dfebabb4feb1.png)<br/>![image](https://user-images.githubusercontent.com/52968530/139148892-b6934608-97d7-444e-beda-17515223b156.png)|

Cada máquina se configuró con los siguientes comandos:
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

## Configuración de DNS
<p align="center"><img width="300px" src="https://user-images.githubusercontent.com/52968530/138371468-5d345846-7aa0-4fff-a884-a691c46493ae.png" /></p>

Ya que tenemos las IP públicas de las máquinas, con el servicio de Freenom se puede solicitar un dominio gratuito. La configuración del DNS queda así:

![image](https://user-images.githubusercontent.com/52968530/139149976-b13fffca-8ee5-46ed-98e4-0dd2e00426b6.png)

## Inicio de los servidores

Aquí se diferencian los dos servidores que se tienen en el mismo repositorio. Por lo que se puede ejecutar uno u otro:

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

Este servidor contiene la página inicial del proyecto con un feed donde se pueden visualizar los proyectos de P1 y P2. La parte visual se realizó de forma manual manteniendo el volumen `wordpress` con esta información.

### `gallery`

Este servidor contiene una galería de distribución aleatoria de los proyectos de P1 y P2. La parte visual se realizó de forma manual manteniendo el volumen `wordpress` con esta información.

### `load balancer`

Este servidor despliega un contenedor `nginx` con la configuración necesaria para tener un balanceador de carga. Dado que el archivo `nginx` no se puede controlar con variables de entorno de forma simple, se creó la configuración específica de cada balanceador (uno por página) y por esto dos carpetas.

## Plugins de Wordpress

En Wordpress e hicieron configuraciones adicionales correspondientes a la instalación de plugins que permitieran configuraciones adicionales como el *Single Sign On* y el *Two Factor Authentication*. Mencionaremos los instalados y una guía oficial que utilizamos para la configuración de los servicios:

### Single Sign On con Auth0
...

### Two Factor Authentication con Auth0
...



## Content Delivery Network (CDN)
<p align="center"><img width="300px" src="https://mma.prnewswire.com/media/1344798/CDN_net_Logo.jpg?p=twitter" /></p>
Utilizamos la prueba gratuita de 14 días de cdn.net, la cuál decidimos solo implementar en la página principal y en un subdominio para simplificar la presentación de lo que se ha implementado.


## Participantes 🚹

|Nombre||
|------|-------|
|David Calle González|<a href="https://github.com/dcalleg707"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/calle_dcg"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
|Juan Sebastián Díaz Osorio|<a href="https://github.com/juansedo"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/juansedo"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
|Santiago Hidalgo Ocampo|<a href="https://github.com/sanhidalgoo"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/sanhidalgoo"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
