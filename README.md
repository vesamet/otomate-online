# Otomate Online
L'Otomate Online est une proposition d'extention pour l'accès/contrôle à distance d'un Otomate.

Cette proposition est constitué de trois choses:
- **Le Collecteur** : il s'agit d'un service installé sur un micro-ordinateur (RaspberryPI 3) que l'on connecte à l'Otomate via sont port usb interne. Le micro-ordinateur est connecté à internet via wifi ou cable ethernet. Cela permet au service de collecter à intervale régulier toute les informations produite par l'Otomate, et de les envoyer sur à un tableau de bord. Le collecteur émet également une interface web accessible par wifi afin de le configurer. Dans une version future, le service sera en mesure de recevoir des commandes issues d'un tableau de bord, afin de les passer À l'Otomate pour qu'elles soit réalisé.

- **Le Tableau de bord**: élément clé de la proposition, le tableau de bord est une application web hébergé sur un serveur cloud sur laquelle il est possible de consulter les informations de l'Otomate, et, éventuellement, délivrer des commandes à distance pour ce dernier.

## Résumé de l'installation envisagée
### Le Collecteur
1. Connecter le Collecteur au port usb de l'Otomate.
1. Connecter le Collecteur a internet:
+ Option 1: connecter un cable **ethernet** au Collecteur.
+ Option 2: se connecter au **réseau wifi** qu'émet le collecteur, et accéder à la page web (collecteur.home). Ensuite, entrez les identifiants du wifi que vous voulez utiliser pour le collecteur dans les champs prévus à cet effet. 
1. (Optionnel) Configurer les options secondaires: intervale de mise à jour, protection par mot de passe, mode veille, etc.

### Le Tableau de bord
1. Installez l'application du tableau de bord sur votre propre **serveur cloud**, ou obtenez-en un sur otomateonline.com
1. Connectez-vous sur votre Tableau de bord et récupérer votre **clé secrète**. 
1. Connectez-vous au wifi du Collecteur et entrez **l'url et la clé secrète** de votre tableau de bord dans les champs prévus à cet effet.
2. Le tour est joué. Vous pouvez maintenant vous connecter à votre tableau de bord et consulter les informations de votre Otomate.

## Aspect technique

### Le Collecteur
Hardware: RaspberryPi version 3
OS: Raspbian
Applications:
- Nodejs (défini l'application de configuration du Collecteur)
- Python (script récupérant les données de l'Otomate pour les inscrire dans un ficher texte.)  
- Nginx (dessert localement la page web de configuration du collecteur)
- Hostapd (dessert la page web de configuration à travers un wifi hotspot)

### Le tableau de bord
Hardware: N'importe quel serveur cloud (AWS, Google Cloud, Azure, etc.) personnel, ou le serveur d'OtomateOnline.com
OS: Ubuntu 18.04
Applications:
- Docker (afin de déployer/distribuer facilement l'ensemble des applications)
- Nodejs & Vuejs (constitut l'application qu'est le tableau de bord)
- Nginx (dessert publiquement le tableau de bord)
- Mysql (store toute les informations délivré par l'Otomate)

