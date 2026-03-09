#  Serveur Multimédia

Utilisation d'un Raspberry Pi comme serveur de streaming multimédia pour accéder à des contenus vidéo et audio depuis n'importe quel appareil du réseau.

---

##  Description

Ce projet installe Jellyfin sur un Raspberry Pi pour créer un serveur multimédia personnel.
Jellyfin permet de streamer films, séries, musique et photos vers des navigateurs web, Smart TV, smartphones et autres appareils.

### Cas d'usage

-  Streaming de films et séries depuis le réseau local
-  Écoute de musique depuis plusieurs appareils
-  Accès depuis smartphone, tablette ou Smart TV
-  Accès à distance via reverse proxy

---

##  Architecture

```
[Navigateur / App Jellyfin / Smart TV]
              │
              │ HTTP / HTTPS
              ▼
     [Raspberry Pi 4]
       └── Jellyfin
             ├── /media/movies     ← Films
             ├── /media/series     ← Séries
             └── /media/music      ← Musique
               (Disque dur externe USB)
```

---

## Technologies utilisées

| Outil | Rôle |
|-------|------|
| **Jellyfin** | Serveur multimédia open source |
| **FFmpeg** | Transcodage audio/vidéo |
| **Nginx**  | Reverse proxy HTTPS |

---

##  Documentation

- [Installation](./installation.md) — Mise en place de Jellyfin
- [Configuration](./configuration.md) — Bibliothèques, utilisateurs et accès

---

## Accès rapide

| Interface | URL |
|-----------|-----|
| Interface web locale | `http://192.168.1.X:8096` |
| Application mobile | Jellyfin sur App Store / Google Play |
| Client TV | Jellyfin pour Android TV, Kodi |


