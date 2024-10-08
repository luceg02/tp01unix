# TP UNIX 
*Luce Giovannetti*

## 2: Post-installation
### 2.3: Nombre de paquets
Pour verifier le nombre de paquets on utilise la commande: 
```bash
dpkg -l | wc -l
   ```
On a 350 paquets.
### 2.4 Space Usage
La racine / repr´esente moins de 1 Go d’espace utilis´e.
On peut le verifier avec la comande : 
```bash
   df -h
   ```
Resultat: 
```bash
Filesystem      Size  Used Avail Use% Mounted on
udev            965M     0  965M   0% /dev
tmpfs           197M  564K  197M   1% /run
/dev/sda1       9.1G  987M  7.7G  12% /
tmpfs           984M     0  984M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/sda2       3.6G   40K  3.4G   1% /tmp
/dev/sda3       921M  281M  577M  33% /var
tmpfs           197M     0  197M   0% /run/user/0
  ```

### 2.5: a indiquer dans le rendu et expliquer les commandes et le resultat obtenu

### 1. Locales
```bash
echo $LANG
```
**Résultat** :
```bash
en_US.UTF-8
```
**Explication** : Cette commande affiche la variable `LANG`, qui définit la langue et la région primaire du système choisie pendant l'installation.

### 2. Nom de la Machine
```bash
hostname
```
**Résultat** :
```bash
serveur1
```
**Explication** : Cette commande affiche le nom de l'hôte (hostname) de la machine choisi pendant l'installation.

### 3. Domaine
```bash
hostname -d
```
**Résultat** :
```bash
ufr-info-p6.jussieu.fr
```
**Explication** : L'option `-d` de la commande `hostname` affiche le domaine de la machine.

### 4. Vérification des Emplacements de Dépôts
```bash
cat /etc/apt/sources.list | grep -v -E '^#|^$'
```
**Résultat** :
```bash
deb http://deb.debian.org/debian/ bookworm main
deb http://security.debian.org/debian-security bookworm-security main
deb http://deb.debian.org/debian/ bookworm-updates main
```
**Explication** : Cette commande liste les dépôts APT configurés dans `/etc/apt/sources.list`, en excluant les lignes de commentaire (lignes commençant par `#`) et les lignes vides, grâce à l'option `grep -v -E '^#|^$'`.

### 5. Passwd/shadow
```bash
cat /etc/shadow | grep -vE ':\*:|:!\*:'
```
**Résultat** :
```bash
root:$y$j9T$5jINqrhEBTA1XXrpknmAr.$C6XsJRuHX7iUQR79U9qtgMRY/pdfyWhmvsYhXJN2dD4:19998:0:99999:7:::
messagebus:!:19998::::::
avahi-autoipd:!:19998::::::
sshd:!:19998::::::
```
**Explication** : Le fichier `/etc/shadow` contient les mots de passe chiffrés des utilisateurs. Cette commande filtre les lignes contenant `*` ou `!*` qui représentent des comptes désactivés ou sans mot de passe.

### 6. Affichage de `/etc/passwd`
```bash
cat /etc/passwd | grep -vE 'nologin|sync'
```
**Résultat** :
```bash
root:x:0:0:root:/root:/bin/bash
```
**Explication** : Le fichier `/etc/passwd` contient les informations sur les utilisateurs. Cette commande exclut les comptes système dont le shell est `nologin` ou `sync`, pour lister uniquement les comptes d’utilisateurs actifs.

### 7. Explication des commandes `fdisk -l` et `fdisk -x`

#### `fdisk -l`
```bash
fdisk -l
```
**Résultat** :
```bash
Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 34366A2F-B417-4C78-A37C-3A0DA762E176

Device        Start      End  Sectors  Size Type
/dev/sda1      2048 19531775 19529728  9.3G Linux filesystem
/dev/sda2  19531776 27344895  7813120  3.7G Linux filesystem
/dev/sda3  27344896 29298687  1953792  954M Linux filesystem
/dev/sda4  29298688 41940991 12642304    6G Linux swap
```
**Explication** : Cette commande liste toutes les partitions de disque sur le système, en affichant des détails sur chaque partition comme la taille, le type de partition, et le système de fichiers.

#### `fdisk -x`
```bash
fdisk -x
```
**Résultat** :
```bash
Disk /dev/sda: 20 GiB, 21474836480 bytes, 41943040 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 34366A2F-B417-4C78-A37C-3A0DA762E176
First usable LBA: 34
Last usable LBA: 41943006
Alternative LBA: 41943039
Partition entries starting LBA: 2
Allocated partition entries: 128
Partition entries ending LBA: 33

Device        Start      End  Sectors Type-UUID                            UUID                                 Name Attrs
/dev/sda1      2048 19531775 19529728 0FC63DAF-8483-4772-8E79-3D69D8477DE4 A1ADE3B5-B2B1-4154-AAE2-289A1344C662 la racine

/dev/sda2  19531776 27344895  7813120 0FC63DAF-8483-4772-8E79-3D69D8477DE4 6BED7E28-1132-488E-B094-0BA55F89E46A espace tempo

/dev/sda3  27344896 29298687  1953792 0FC63DAF-8483-4772-8E79-3D69D8477DE4 3D71B75B-D723-44CA-B1D9-A0A1C0C24AAC les logs

/dev/sda4  29298688 41940991 12642304 0657FD6D-A4AB-43C4-84E5-0933C84B4F4F 471EF37B-8046-49C0-BB15-4EB652660804 ma swap
```
**Explication** : La commande `fdisk -x` est parfois utilisée pour afficher des informations plus détaillées sur les partitions, notamment sur le type UUID, les attributs, et les informations de partitioning GPT.

### 8. Explication de la commande `df -h`
```bash
df -h
```
**Résultat** :
```bash
Filesystem      Size  Used Avail Use% Mounted on
udev            965M     0  965M   0% /dev
tmpfs           197M  564K  197M   1% /run
/dev/sda1       9.1G  987M  7.7G  12% /
tmpfs           984M     0  984M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/sda2       3.6G   40K  3.4G   1% /tmp
/dev/sda3       921M  278M  580M  33% /var
tmpfs           197M     0  197M   0% /run/user/0
```
**Explication** : Cette commande affiche l'utilisation de l'espace disque pour tous les systèmes de fichiers montés. L'option `-h` (human-readable) permet d'afficher les tailles dans un format lisible, et le résultat inclut la capacité totale, l’espace utilisé, l’espace libre et le point de montage de chaque système de fichiers.

## 3. Aller plus loin

### 3.1 Installation automatique : Preseed

**Preseed** est un système utilisé pour automatiser l'installation de systèmes d'exploitation basés sur Debian en fournissant les réponses aux questions posées durant l'installation via un fichier de configuration. Ce fichier contient des paramètres qui configurent automatiquement les options d'installation, comme le partitionnement, la langue, les comptes utilisateurs, et les paramètres réseau.

- **Utilisation** : Le fichier preseed est placé sur un serveur ou une clé USB, et il est lu par le programme d’installation. On peut, par exemple, configurer des installations de masse pour plusieurs serveurs sans intervention manuelle.
  
- **Documentation** : [Debian Preseed Documentation](https://wiki.debian.org/DebianInstaller/Preseed).


### 3.2 Rescue Mode : Réinitialisation du mot de passe root
Il est possible de le réinitialiser en utilisant le **mode rescue**. Voici les étapes:
1. **Redémarrer le système** et accéder au menu de GRUB.
2. Dans GRUB, appuyer sur `e` pour éditer les paramètres de démarrage.
3. Ajouter `init=/bin/bash` à la fin de la ligne qui commence par `linux`.
4. Appuyer sur `Ctrl + X` pour démarrer avec cette configuration.
5. Remonter la partition en lecture/écriture avec :
   ```bash
   mount -o remount,rw /
   ```
6. Réinitialiser le mot de passe root :
```bash
   passwd root
   ```
7. Entrer un nouveau mot de passe et redémarrer le système :
```bash
 reboot
   ```

- **Documentation** : https://linuxconfig.org/recover-reset-forgotten-linux-root-password , https://raspberrytips.com/reset-password-linux/

### 3.3 Redimentionnement partition
#### Avant de redimentionner notre partition racine:
1. Sauvegarder toutes donnes importantes avant de commencer la modification.
2. Démarrer à partir d'un live CD/USB pour éviter toute probleme.
   
#### Maintenant on peut:
1. Démarrer la machine avec le live USB 
3. Selectionner la partition racine `/dev/sda1`.
4. Selectionner **"Redimensionner/Déplacer"** pour appliquer les changements.
5. Après le redimensionnement, vérifier l'etat du systeme de fichier avec:
```bash
 e2fsck -f /dev/sdaX
```
- **Documentation** : https://www.baeldung.com/linux/resize-partitions , https://gparted.org/display-doc.php?name=moving-space-between-partitions
