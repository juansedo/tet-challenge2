# Proyecto 2 - Tópicos especiales en Telemática 📶

En este documento se explicará con detalle técnico el desarrollo de este proyecto, así como los pasos para instalarse y poder replicar nuestros resultados.

Este proyecto fue desarrollado en GCP con algunas de sus herramientas por lo que los nombres harán referencias a configuraciones de esta plataforma, pero puede hacerse lo mismo en otras IaaS.

## Diseño lógico de la implementación
...

## Diseño técnico de la implementación
...

## Configuración e inicialización de instancias

<p align="center"><img src="https://user-images.githubusercontent.com/52968530/138364996-75e63672-050f-453d-999f-475aaf4b5547.png" /></p>

Utilizando el Compute Engine de GCP, montamos las instancias de VM para nuestra infraestructura. Las VM implementadas son los `main` servers, los `gallery` servers y los `load-balancer` servers.

Para los load balancer, la configuración de disco y de firewall es esta:

![image](https://user-images.githubusercontent.com/52968530/138375330-1400117b-c5c0-4567-8c17-67f6f63a79f1.png)
![image](https://user-images.githubusercontent.com/52968530/138375347-1d09db93-65f7-4d77-8d24-8ef10789b5e6.png)

Ya en cada máquina, los comandos de configuración inicial son:
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
<p align="center"><img src="https://user-images.githubusercontent.com/52968530/138371468-5d345846-7aa0-4fff-a884-a691c46493ae.png" /></p>

Ya que tenemos las IP públicas de las máquinas, con el servicio de Freenom se puede solicitar un dominio. Luego de conseguirlo, la configuración del DNS queda así:

![image](https://user-images.githubusercontent.com/52968530/138375204-f15e97eb-038c-4275-bb13-1894179da6ba.png)

Siendo 34.125.43.6 la IP de nuestro `main-server` y 34.125.252.186 la IP de nuestro `gallery-server`.

## Inicio de los servidores

Aquí se diferencian los dos servidores que se tienen en el mismo repositorio. Por lo que se puede ejecutar uno u otro:

```
# Starting main-server
cd tet-challenge2/main-server/
cp .env.example .env
sudo docker-compose up -d

# Starting gallery-server
cd tet-challenge2/gallery-server/
cp .env.example .env
sudo docker-compose up -d
```

### `main-server`

Este servidor contiene la página inicial del proyecto con un feed donde se pueden visualizar los proyectos de P1 y P2. La parte visual se realizó de forma manual manteniendo el volumen `wordpress` con esta información.

### `gallery-server`

Este servidor contiene una galería de distribución aleatoria de los proyectos de P1 y P2. La parte visual se realizó de forma manual manteniendo el volumen `wordpress` con esta información.



## Participantes 🚹

|Nombre||
|------|-------|
|David Calle González|<a href="https://github.com/dcalleg707"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/calle_dcg"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
|Juan Sebastián Díaz Osorio|<a href="https://github.com/juansedo"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/juansedo"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
|Santiago Hidalgo Ocampo|<a href="https://github.com/sanhidalgoo"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/sanhidalgoo"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
