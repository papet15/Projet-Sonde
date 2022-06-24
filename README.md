
Projet sonde@mo
Spécifications fonctionnelles
1. Présentation
Le principe du projet est de fabriquer une sonde WiFi de température et pression
type Netatmo qui puisse s'intégrer dans un environnement domestique.
Elle pourra donner les informations météo en direct via une API web mais
également un historique de mesures sur les jours, semaines, mois et années précédentes.
Robuste, sonde@mo résiste aux contraintes d’un appareil grand public (CE)
notamment les coupures de courant et arrêts brutaux.
Idéalement, sonde@mo pourra aussi s’intégrer dans des environnements existants
type IFTTT et proposer une API.
2. Exigences
○ Sonde de pression et température
Les informations de température et pression sont acquises par un capteur
i2c BMP180 ou BME280.
○ Historique des mesures
Les mesures sont horodatées et archivées dans une base de données sur
une partition RW de notre système à une granularité temporelle de N
minutes. On pourra configurer N par l’interface web par exemple.
○ API web
Une API web embarquée dans notre sonde permet de :
● la configurer (granularité, WiFi, autres services, etc)
● récupérer la température en direct avec les min et max du jour
● consulter et télécharger (CSV ou JSON) l’historique des mesures
○ Robustesse
Le produit prend en compte les modes d'utilisation grand public (coupure de
courant et arrêts brutaux). Il est donc majoritairement en lecture seule pour
éviter les corruptions de fichiers. Une partition RW pourra être ajoutée pour
stocker les données persistantes (configurations, mesures, etc).
Version 2.2 du 22/06/2022
○ Intégration WiFi domestique
La sonde pourra se comporter comme point d’accès WiFi en mode nominal
et pourra être configurée comme client sur un réseau WiFi domestique (via
une IHM web).
○ Mise à l’heure
La sonde se met à l’heure automatiquement par NTP en utilisant le WiFi
domestique.
○ Signalétique
La sonde utilise une led heartbeat pour indiquer son état de santé.
○ Reset usine
Une pression 10s sur un bouton poussoir permet de remettre la sonde à
l’état usine (WiFi, configurations, mesures, etc).
○ Exploitation graphique via client lourd
Un client lourd C++/QT pourra requêter l’historique des mesures par API
dédiée (REST ou autre) et afficher des graphiques de ces mesures, des
tendances, les extrêmes annuels...
Il permettra également de configurer la sonde via son API web.
3. Technologies recommandées
○ Raspberry Pi OS voir Buildroot dans un second temps
○ Système léger et lecture-seule
○ 3ème partition RW EXT4 pour les données persistantes
○ Base de données SQLite
○ Serveur web léger type Lighttpd
○ Backoffice C (CGI) pour l’API REST
○ Suivi de révisions GIT
4. Organisation du travail
Vous devrez livrer avant de commencer à développer :
○ Conception Générale du système
○ Conception Logicielle (UML avec classes, méthodes et attributs)
Les autres critères suivants sont obligatoires :
○ Mise en place de tests unitaires
○ Équipes de 1 ou de 2
Version 2.2 du 22/06/2022
5. Autres fonctionnalités envisageables
○ Intégration service cloud IFTTT
○ Notification Android/IOS en cas de dépassement de température (ex :
plateforme cloud type Pushover)
○ API HTTP REST publique pour intégration de la sonde dans d’autres
systèmes (domotique, etc) bien qu’elle soit peut être nécessaire pour traiter
l’exigence Exploitation graphique via client lourd
○ Exploitation web plus complète avec graphe des mesures
○ Sortie HDMI avec QT pour connecter la sonde à un écran et y afficher la
température en direct
○ Gestion d’un écran OLED pour afficher
○ Mise à jour OTA (Over the Air)
○ ...
Version 2.2 du 22/06/2022

