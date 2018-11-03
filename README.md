# Installation de la vidéo sur le rasp

## Pré-requis

- Mettre à jour le rasp

````bash
sudo apt-get update -y && sudo apt-get upgrade -y
````

- Installation de motion sur le rasp :
````bash
sudo apt-get install motion
````

- Installation de nginx
````bash
sudo apt-get install nginx
````

## Configuration

### Motion

- Copier les les fichiers situés dans ``/rasp/motion`` dans ``/etc/motion``
- Modifier les fichiers ``salon.conf`` et ``jardin.conf`` avec les identifiants des cameras

### Nginx

- Copier le contenu de ``/rasp/html`` dans ``/var/www/html``

### Lancer les services

````bash
sudo motion start
sudo service nginx start
````

### Automatiser l'activation / désactivation de la détection

````bash
sudo crontab -e
````

````
00 22 * * * /usr/bin/curl http://localhost:8080/1/detection/start
00 8 * * * /usr/bin/curl http://localhost:8080/1/detection/pause
00 8 * * 1-5 /usr/bin/curl http://localhost:8080/2/detection/start
30 17 * * 1-5 /usr/bin/curl http://localhost:8080/2/detection/pause
````