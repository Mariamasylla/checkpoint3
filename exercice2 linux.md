**Partie 2 : Configuration de SSH**

Q.2.1.1 - Créer un compte personnel

sudo adduser Mariama
<img width="449" alt="1 1" src="https://github.com/user-attachments/assets/a6b212b2-6e56-4238-bb50-ee54ab46d8af" />


Q.2.1.2 - je  Préconise pour ce compte
Mot de passe sécurisé : au moins 12 caractères avec majuscules, minuscules, chiffres et caractères spéciaux.

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


Q.2.3.2 Le type de système de stockage qu' ils utilisent 
  
  Taper: lsblk 


Q.2.3.3  Nouveau disque de 8,00 Gio au serveur et réparer le volume RAID
 
 sudo mdadm --add /dev/md0 /dev/sdb et verifier son etat en tapant cat /proc/mdstat



Q.2.3.4 Nouveau volume logique LVM de 2 Gio qui servira à héberger des sauvegardes et  doit être monté automatiquement à chaque démarrage dans l'emplacement par défaut : /var/lib/bareos/storage.

sudo lvcreate -L 2G -n sauvegarde debian-vg
sudo mkdir -p /var/lib/bareos/storage


Q.2.3.5 Espace disponible  dans le groupe de volume 

vgdisplay
