# NAS Server — Configuration

Ce guide couvre la configuration avancée du NAS, la gestion des utilisateurs et les bonnes pratiques.

---

## 1. Gestion des utilisateurs

### Ajouter un nouvel utilisateur système

```bash
sudo adduser nom_utilisateur
sudo smbpasswd -a nom_utilisateur
```

### Donner accès à un partage spécifique

Dans `/etc/samba/smb.conf`, modifier la ligne `valid users` du partage concerné :

```ini
valid users = pi, nom_utilisateur
```

Redémarrer Samba :

```bash
sudo systemctl restart smbd
```

### Supprimer un utilisateur Samba

```bash
sudo smbpasswd -x nom_utilisateur
```

---

## 2. Surveillance de l'espace disque

### Vérifier l'espace disponible

```bash
df -h /mnt/nas
```

### Connaître la taille des sous-dossiers

```bash
du -sh /mnt/nas/*
```

### Automatiser un rapport hebdomadaire par email

```bash
crontab -e
```

Ajouter :

```
0 8 * * 1 df -h /mnt/nas | mail -s "Rapport NAS" votre@email.com
```

---

## 3. Accès à distance sécurisé

### Via SSH Tunneling

Depuis un réseau externe, rediriger le port SMB via SSH :

```bash
ssh -L 4455:localhost:445 pi@VOTRE_IP_PUBLIQUE
```

Puis accéder au NAS via `\\localhost:4455\shared`.

### Via WireGuard 

Installer WireGuard pour créer un VPN et accéder au NAS comme si vous étiez sur le réseau local :

```bash
sudo apt install wireguard -y
```
suite sur la configuration du site officiel

