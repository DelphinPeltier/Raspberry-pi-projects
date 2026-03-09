#  Serveur NAS

Utilisation d'un Raspberry Pi comme serveur de stockage réseau (NAS) pour centraliser et partager des fichiers sur le réseau local et à distance.

---

##  Description

Ce projet transforme un Raspberry Pi en NAS (*Network Attached Storage*) accessible depuis n'importe quel appareil du réseau local. 
Il permet de stocker, organiser et partager des fichiers sans dépendre d'un service cloud tiers.

### Cas d'usage

-  Partage de fichiers entre PC, Mac, smartphones et tablettes
-  Sauvegarde automatique des appareils du réseau
-  Accès à distance sécurisé via VPN ou SFTP
-  Stockage centralisé de photos et vidéos

---

##  Architecture

```
[PC / Mobile]
        │
        │ SMB / SFTP / HTTP
        ▼
[Raspberry Pi 4]
  ├── Samba (partage réseau local)
  ├── OpenSSH (accès SFTP)
  └── [Disque dur externe USB]
        ├── /shared       ← Dossier partagé
        ├── /backups      ← Sauvegardes
        └── /media        ← Médias
```

---

##  Technologies utilisées

| Outil | Rôle |
|-------|------|
| **Samba** | Partage de fichiers via le protocole SMB (Windows, macOS, Linux) |
| **OpenSSH / SFTP** | Accès sécurisé et transfert de fichiers à distance |
| **ext4 / exFAT** | Système de fichiers du disque externe |
| **udev** | Montage automatique du disque USB |

---

##  Documentation

- [Installation](./installation.md) — Mise en place du serveur NAS
- [Configuration](./configuration.md) — Paramétrage des partages et des accès

---

##  Accès rapide

| Service | URL / Commande |
|---------|----------------|
| Partage réseau | `\\192.168.1.X\shared` (Windows) |
| Accès SFTP | `sftp pi@192.168.1.X` |
