# NAS Server — Installation

Ce guide décrit l'installation complète d'un serveur NAS sur Raspberry Pi avec Samba.

---

## Prérequis

- Raspberry Pi OS Lite 64-bit installé
- Accès SSH au Raspberry Pi
- Disque dur externe USB formaté
- IP statique configurée (ex. `192.168.1.50`)

---

## 1. Mise à jour du système

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2. Préparation du disque externe

### 2.1 Identifier le disque

```bash
lsblk
```

Le disque externe apparaît généralement sous `/dev/sda`.

### 2.2 Formater le disque (si nécessaire)

> ⚠️ **Cette opération efface toutes les données du disque.**

```bash
sudo mkfs.ext4 /dev/sda1
```

### 2.3 Créer le point de montage

```bash
sudo mkdir -p /mnt/nas
```

### 2.4 Récupérer l'UUID du disque

```bash
sudo blkid /dev/sda1
```

Notez l'UUID affiché, ex. : `UUID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"`

### 2.5 Configurer le montage automatique

```bash
sudo nano /etc/fstab
```

Ajouter la ligne suivante à la fin du fichier :

```
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  /mnt/nas  ext4  defaults,nofail  0  2
```

### 2.6 Monter le disque

```bash
sudo mount -a
```

Vérifier le montage :

```bash
df -h | grep /mnt/nas
```

---

## 3. Création de la structure de dossiers

```bash
sudo mkdir -p /mnt/nas/{shared,backups,media}
sudo chown -R pi:pi /mnt/nas
sudo chmod -R 775 /mnt/nas
```

---

## 4. Installation de Samba

### 4.1 Installer le paquet

```bash
sudo apt install samba samba-common-bin -y
```

### 4.2 Sauvegarder la configuration par défaut

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
```

### 4.3 Configurer Samba

```bash
sudo nano /etc/samba/smb.conf
```

Ajouter à la fin du fichier :

```ini
[shared]
   path = /mnt/nas/shared
   browseable = yes
   writable = yes
   only guest = no
   create mask = 0775
   directory mask = 0775
   valid users = pi

[backups]
   path = /mnt/nas/backups
   browseable = yes
   writable = yes
   only guest = no
   create mask = 0660
   directory mask = 0770
   valid users = pi

[media]
   path = /mnt/nas/media
   browseable = yes
   writable = yes
   only guest = no
   create mask = 0775
   directory mask = 0775
   valid users = pi
```

### 4.4 Créer un utilisateur Samba

```bash
sudo smbpasswd -a pi
```

Saisir et confirmer un mot de passe.

### 4.5 Vérifier la configuration

```bash
testparm
```

### 4.6 Redémarrer Samba

```bash
sudo systemctl restart smbd nmbd
sudo systemctl enable smbd nmbd
```

---

## 5. Vérification

Depuis un autre appareil du réseau, tenter d'accéder au partage :

- **Windows** : `\\192.168.1.50\shared` dans l'explorateur de fichiers
- **Linux** : `smb://192.168.1.50/shared` dans le gestionnaire de fichiers

---

## 6. (Optionnel) Installation de SFTP

SSH est déjà actif sur Raspberry Pi OS. SFTP est inclus dans OpenSSH. Aucune installation supplémentaire n'est requise.

Se connecter via SFTP :

```bash
sftp pi@192.168.1.50
```

---

## ✅ Résumé des services installés

| Service | Port | Protocole |
|---------|------|-----------|
| Samba (SMB) | 445 | TCP |
| NetBIOS | 137-139 | TCP/UDP |
| SFTP | 22 | TCP |
