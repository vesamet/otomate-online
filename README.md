# 🗜️ Otomate Online
**L'Otomate Online** est une proposition d'extention pour l'accès/contrôle à distance d'un Otomate.

Cette proposition est constitué de trois choses:
- **Le Collecteur** : il s'agit d'un service installé sur un micro-ordinateur (RaspberryPI 3) que l'on connecte à l'Otomate via sont port usb interne. Le micro-ordinateur est connecté à internet via wifi ou cable ethernet. Cela permet au service de collecter à intervale régulier toute les informations produite par l'Otomate, et de les envoyer à un tableau de bord. Le collecteur émet également une interface web accessible par wifi afin de le configurer. Dans une version futur, le service sera en mesure de recevoir des commandes issues d'un tableau de bord, afin de les passer à l'Otomate pour qu'elles soit réalisé.

- **Le Tableau de bord**: élément clé de la proposition, le tableau de bord est une application web hébergé sur un serveur cloud sur laquelle il est possible de consulter les informations de l'Otomate, et, éventuellement, délivrer des commandes à distance pour ce dernier.

![aperçu du tableau de bord](https://i.ibb.co/6sk64vQ/7cd818f022fb4daca979c7265495b3cf.png)

## 🧭 Résumé de l'installation envisagée
### Le Collecteur
1. Connecter le Collecteur au port usb de l'Otomate.
1. Connecter un cable ethernet au Collecteur.
1. Connecter le cable d'alimentation au port usb-micro du Collecteur.

### Le Tableau de bord
1. Installez l'application du tableau de bord sur votre propre **serveur cloud**, ou obtenez-en un sur otomateonline.com
1. Connectez-vous sur votre Tableau de bord et entrez **l'id** et la **clé secrète** du Collecteur.
1. Attendez 5 à 10 min, et le tour est joué! 

## ⚙️ Aspects techniques

### Le Collecteur
**Hardware:** RaspberryPi version 3

**OS:** Raspbian

**Applications:**
- Nodejs (défini l'application de configuration du Collecteur)
- Python(?) (script récupérant les données de l'Otomate pour les inscrire dans un ficher texte.)  
- Nginx (dessert localement la page web de configuration du collecteur)
- Hostapd (dessert la page web de configuration à travers un wifi hotspot)

**Fonctionnalités planifiées:**
- Il est défini par un id, une clé secrète unique ainsi que l'adresse du serveur ou se trouve le tablau de bord, ce qui lui sert d'identifiant pour être reconnu par se dernier.
- Il peut envoyer les données de l'Otomate au tableau de bord.
- Il envoie une requête à interval régulier au tableau de bord pour y récupérer des commandes ou mises à jour sysème.

### Le tableau de bord
**Hardware:** N'importe quel serveur cloud (AWS, Google Cloud, Azure, etc.) personnel, ou le serveur d'OtomateOnline.com

**OS:** Ubuntu 18.04

**Applications:**
- Docker (afin de déployer/distribuer facilement l'ensemble des applications)
- Nodejs & Vuejs (constitut l'application qu'est le tableau de bord)
- Nginx (dessert publiquement le tableau de bord)
- Mysql (store toute les informations délivré par l'Otomate)

**Fonctionnalités planifiées:**
- Reçois et répond aux requêtes du Collecteur et classifie les données reçu dans un base de donnée.
- Affiche dans un tableau de bord les-dites données de manière claire et éléguante.
- Récupère et prépare les commandes destinée à l'Otomate, afin que le Collecteur puisse les demander.

