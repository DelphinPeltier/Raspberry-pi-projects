#  Home Assistant

Mise en place d'un **serveur domotique** avec Home Assistant sur Raspberry Pi pour automatiser des équipements et centraliser le contrôle de la maison connectée.

---

##  Description

[Home Assistant](https://www.home-assistant.io/) est une plateforme domotique open source qui permet d'intégrer, de contrôler et d'automatiser des équipements connectés de nombreuses marques différentes 
(Philips Hue, IKEA Trådfri, Sonoff, Xiaomi, etc.) depuis une interface unifiée.

### Cas d'usage

-  Contrôle de l'éclairage connecté
-  Gestion de serrures connectées 
-  Automatisations basées sur l'heure, la présence ou des capteurs
-  Tableaux de bord personnalisés (dashboards)
-  Notifications sur smartphone

---

##  Architecture

```
[Smartphone / Tablette / Navigateur]
              │
              │ HTTP / HTTPS
              ▼
     [Raspberry Pi 4]
       └── Home Assistant
             ├── Intégrations
             │     ├── Philips Hue (Zigbee)
             │     └── Google Home
             │  
             └── Automations
```

---

##  Technologies utilisées

| Outil | Rôle |
|-------|------|
| **Home Assistant OS** | Système domotique complet |
| **Zigbee2MQTT** (optionnel) | Intégration d'appareils Zigbee via clé USB |

---

##  Documentation

- [Installation](./installation.md) — Installation de Home Assistant OS
- [Configuration](./configuration.md) — Intégrations, automatisations et dashboards

---

## Accès rapide

| Interface | URL |
|-----------|-----|
| Interface web locale | `http://homeassistant.local:8123` |
| IP directe | `http://192.168.1.X:8123` |
| Application mobile | Home Assistant sur App Store / Google Play |

