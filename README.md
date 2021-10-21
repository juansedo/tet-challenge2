# Proyecto 2 - Tópicos especiales en Telemática 📶

En este documento se explicará con detalle técnico el desarrollo de este proyecto, así como los pasos para instalarse y poder replicar nuestros resultados.

Este proyecto fue desarrollado en GCP con algunas de sus herramientas por lo que los nombres harán referencias a configuraciones de esta plataforma, pero puede hacerse lo mismo en otras IaaS.

## Configuración e inicialización de instancias

Al acceder a GCP, ...

Los comandos más fundamentales son:
```
# Updating system
sudo apt update -y && sudo apt upgrade -y
sudo apt install wget -y
sudo apt install git -y

# Installing docker and docker-compose 
sudo wget -O - https://bit.ly/docker-install | bash

# Downloading the project
git clone https://github.com/juansedo/tet-challenge2.git

# Starting the project 
cd tet-challenge2
cp .env.example .env
sudo docker-compose up -d
```

## Participantes 🚹

|Nombre||
|------|-------|
|David Calle González|<a href="https://github.com/dcalleg707"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/calle_dcg"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
|Juan Sebastián Díaz Osorio|<a href="https://github.com/juansedo"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/juansedo"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|
|Santiago Hidalgo Ocampo|<a href="https://github.com/sanhidalgoo"><img src="https://image.flaticon.com/icons/png/512/25/25231.png" width=20></a> <a href="https://instagram.com/sanhidalgoo"><img src="https://cdn-icons-png.flaticon.com/512/174/174855.png" width=20></a>|