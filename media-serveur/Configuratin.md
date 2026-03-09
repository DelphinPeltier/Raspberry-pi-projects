#  Serveur Multimédia — Configuration

---

## 1. Configuration du transcodage

### Activer l'accélération matérielle

Sur Raspberry Pi 4, l'accélération V4L2 est disponible :

```
Tableau de bord > Lecture > Transcodage
```

- Accélération matérielle : `V4L2 (Raspberry Pi)`
- Décodage matériel : activer H.264, HEVC si supporté

>  Le transcodage matériel améliore les performances mais peut être instable selon les versions.

### Qualité de streaming par défaut

```
Tableau de bord > Lecture > Qualité de lecture par défaut
```

Recommandé pour Raspberry Pi 4 : 20 Mbps en local, 4 Mbps pour un accès distant.

---

## 2. Accès à distance avec Nginx (HTTPS)

### Installer Nginx et Certbot

```bash
sudo apt install nginx certbot python3-certbot-nginx -y
```

### Configurer le virtual host

```bash
sudo nano /etc/nginx/sites-available/jellyfin
```

```nginx
server {
    listen 80;
    server_name jellyfin.votredomaine.com;

    location / {
        proxy_pass http://localhost:8096;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_buffering off;
        proxy_read_timeout 600s;
    }
}
```

```bash
sudo ln -s /etc/nginx/sites-available/jellyfin /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
```

### Obtenir un certificat SSL

```bash
sudo certbot --nginx -d jellyfin.votredomaine.com
```

---

## 3. Notifications et plugins

### Activer un plugin

```
Tableau de bord > Plugins > Catalogue
```

Plugins recommandés :

| Plugin | Description |
|--------|-------------|
| Jellyseerr | Système de demande de médias |
| Fanart | Amélioration des visuels |
| Trakt | Synchronisation des films vus |
