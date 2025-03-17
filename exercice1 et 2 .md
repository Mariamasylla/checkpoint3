**Partie1**

Q.2.1.1 - Créer un compte personnel

sudo adduser Mariama
<img width="449" alt="1 1" src="https://github.com/user-attachments/assets/a6b212b2-6e56-4238-bb50-ee54ab46d8af" />


Q.2.1.2 - je  Préconise pour ce compte
Mot de passe sécurisé : au moins 12 caractères avec majuscules, minuscules, chiffres et caractères spéciaux.

**Partie 2 : Configuration de SSH**
Q.2.2.1 - Désactiver complètement l'accès à distance de root



sudo nano /etc/ssh/sshd_config

PermitRootLogin non
<img width="419" alt="desactiver root" src="https://github.com/user-attachments/assets/a017c4de-a168-4314-bcf2-97f957c0bacd" />

Q.2.2.2 Autoriser l'accès à distance à ton compte personnel uniquement.

Dans le fichier /etc/ssh/sshd_config, ajouter la ligne AllowUsers Mariama

Q.2.2.3 Mettre en place une authentification par clé valide et désactiver l'authentification par mot de passe

<img width="448" alt="authentification par clé" src="https://github.com/user-attachments/assets/db920ffb-3c4b-4a9b-85af-c20ea0d7aa2f" />

**Partie 3 : Analyse du stockage**
Q.2.3.1 Les systèmes de fichiers actuellement montés 

df -hT
<img width="400" alt="image" src="https://github.com/user-attachments/assets/e8e476e8-4e42-4e6a-bd8f-d11438cfb834" />



Q.2.3.2 Le type de système de stockage qu' ils utilisent 
  
  Taper: lsblk 


Q.2.3.3  Nouveau disque de 8,00 Gio au serveur et réparer le volume RAID
 
 sudo mdadm --add /dev/md0 /dev/sdb et verifier son etat en tapant cat /proc/mdstat



Q.2.3.4 Nouveau volume logique LVM de 2 Gio qui servira à héberger des sauvegardes et  doit être monté automatiquement à chaque démarrage dans l'emplacement par défaut : /var/lib/bareos/storage.

sudo lvcreate -L 2G -n sauvegarde debian-vg
sudo mkdir -p /var/lib/bareos/storage


Q.2.3.5 Espace disponible  dans le groupe de volume 

vgdisplay

**Partie 4 : Sauvegardes**


Q.2.4.1  les rôles respectifs des 3 composants bareos installés sur la VM.


**Bareos Director**  est responsable de la planification, du contrôle et du lancement des tâches de sauvegardes. 
**Bareos File Daemon** est en charge de collecter les informations à sauvegarder et de les envoyer au Bareos Storage Daemon
**Bareos Storage Daemon** permet d'effectuer des sauvegardes sur différents types de supports 

**Partie 5 : Filtrage et analyse réseau**
Q.2.5.1Les règles appliquées sur Netfilter 

<img width="416" alt="image" src="https://github.com/user-attachments/assets/f463de58-7174-48d1-b721-ed77cee3ffc8" />


Q.2.5.2 Les types de communications  autorisées 

Q.2.5.3 Quels types sont interdit ?

Q.2.5.4 Sur nftables, ajouter les règles nécessaires pour autoriser bareos à communiquer avec les clients bareos potentiellement présents sur l'ensemble des machines du réseau local sur lequel se trouve le serveur


**Partie 6 : Analyse de logs**
Q.2.6.1 Lister les 10 derniers échecs de connexion ayant eu lieu sur le serveur en indiquant pour chacun :

La date et l'heure de la tentative
L'adresse IP de la machine ayant fait la tentative
<img width="413" alt="image" src="https://github.com/user-attachments/assets/a12ea941-b1a7-407c-ad88-6c019c23e9d0" />




**Exercice 1 : Manipulations pratiques sur VM Windows**

**Partie 1 : Gestion des utilisateurs**

Q.1.1.1 Créer l'utilisateur Lionel Lemarchand avec les même attribut de société que Kelly Rhameur.


<img width="473" alt="image" src="https://github.com/user-attachments/assets/3270d4e1-be72-4a95-8b0a-34c4813adcaa" />


Q.1.1.2 Créer une OU DeactivatedUsers et déplace le compte désactivé de Kelly Rhameur dedans.

<img width="485" alt="image" src="https://github.com/user-attachments/assets/6e633eb0-ac95-4715-aee1-ba0042b6c24f" />


Q.1.1.3 Modifier le groupe de l'OU dans laquelle était Kelly Rhameur en conséquence.

<img width="485" alt="image" src="https://github.com/user-attachments/assets/8a107058-8f33-4d5a-b5e8-30df13b40a14" />



Q.1.1.4 Créer le dossier Individuel du nouvel utilisateur et archive celui de Kelly Rhameur en le suffixant par -ARCHIVE.


**Partie 2 : Restriction utilisateurs**

Q.1.2.1 Faire en sorte que l'utilisateur Gabriel Ghul ne puisse se connecter que du lundi au vendredi, de 7h à 17h.

<img width="416" alt="image" src="https://github.com/user-attachments/assets/cc9173a3-85a5-4bce-b20f-46ad12817fc3" />


Q.1.2.2 De même, bloquer sa connexion au seul ordinateur CLIENT01.

<img width="419" alt="image" src="https://github.com/user-attachments/assets/bb75d4d1-0996-431a-b84d-c627fc3e492c" />


Q.1.2.3 Mettre en place une stratégie de mot de passe pour durcir les comptes des utilisateurs de l'OU LabUsers






**Partie 3 : Lecteurs réseaux**
Q.1.3.1 Créer une GPO Drive-Mount qui monte les lecteurs E: et F: sur les clients.



<img width="410" alt="image" src="https://github.com/user-attachments/assets/a621847c-1b37-4597-a135-196e287490fb" />


