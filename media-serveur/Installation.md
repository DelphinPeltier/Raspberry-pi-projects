# Serveur Multimédia — Installation

---

## 1. Installation des dépendances

```bash
sudo apt install apt-transport-https ca-certificates curl gnupg -y
```

---

## 2. Ajout du dépôt Jellyfin

```bash
curl -fsSL https://repo.jellyfin.org/ubuntu/jellyfin_team.gpg.key \
  | sudo gpg --dearmor -o /usr/share/keyrings/jellyfin.gpg

echo "deb [signed-by=/usr/share/keyrings/jellyfin.gpg] \
  https://repo.jellyfin.org/ubuntu jammy main" \
  | sudo tee /etc/apt/sources.list.d/jellyfin.list
```

---

## 3. Installation de Jellyfin

```bash
sudo apt update
sudo apt install jellyfin -y
```

---

## 4. Démarrage et activation du service

```bash
sudo systemctl start jellyfin
sudo systemctl enable jellyfin
```

Vérifier que le service est actif :

```bash
sudo systemctl status jellyfin
```

---

## 5. Préparation du disque multimédia

### 5.1 Monter le disque externe

```bash
sudo mkdir -p /mnt/media
sudo mount /dev/sda1 /mnt/media
```

Montage automatique via `/etc/fstab`.

### 5.2 Organiser les médias

```bash
sudo mkdir -p /mnt/media/{movies,series,music,photos}
```

### 5.3 Permissions

```bash
sudo chown -R jellyfin:jellyfin /mnt/media
sudo chmod -R 755 /mnt/media
```

---

## 6. Installation de FFmpeg

FFmpeg est nécessaire pour le transcodage vidéo :

```bash
sudo apt install ffmpeg -y
```

---

## 7. Configuration initiale via le navigateur

1. Depuis un autre appareil du réseau, ouvrir : `http://192.168.1.51:8096`
2. Suivre l'assistant de configuration :
   - Créer un compte administrateur
   - Choisir la langue
   - Ajouter les bibliothèques multimédia (pointant vers `/mnt/media/movies`, etc.)
3. Attendre l'indexation des médias

---

## Résumé

| Service | Port | Description |
|---------|------|-------------|
| Jellyfin Web | 8096 | Interface principale HTTP |
| DLNA | 1900 | Découverte réseau (UDP) |
