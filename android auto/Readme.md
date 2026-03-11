#  Android Auto — Interface embarquée sur Raspberry Pi

Expérimentation d'une **interface multimédia embarquée pour voiture** en connectant un Raspberry Pi à un écran dans l'habitacle.

---

##  Description

Ce projet explore la création d'un système multimédia embarqué DIY en utilisant un Raspberry Pi connecté à un écran tactile dans une voiture. 
L'objectif est d'expérimenter avec un système embarqué Linux dans un contexte contraint (alimentation, température, démarrage rapide).

Pour le projet, on utilisera :
- **OpenAuto** : solution open source

### Cas d'usage

-  Navigation GPS
-  Lecture de musique via Android Auto (mirroring)
-  Intégration smartphone via USB ou Bluetooth
-  Interface tactile personnalisable

---

##  Architecture

```
[Smartphone Android]
        │
        │ USB / Bluetooth (Android Auto / AA Wireless)
        ▼
[Raspberry Pi 4]
  ├── OpenAuto Pro / Crankshaft
  ├── Écran tactile 7" (HDMI + USB)
  ├── Alimentation stepdown 12V → 5V
  └── Carte son Jack
        │
        ▼
   [Autoradio / AUX]
```

---

##  Matériel requis

| Composant | Description |
|-----------|-------------|
| Raspberry Pi 4 (2 Go min.) | Unité centrale |
| Écran tactile 7" HDMI | Affichage et interaction |
| Convertisseur DC-DC 12V → 5V 3A | Alimentation depuis la batterie voiture |
| Câble USB-A vers USB-C | Connexion smartphone |
| Boîtier de protection | Fixation et protection thermique |
| Câble AUX 3.5mm | Sortie audio vers autoradio |

---

##  Technologies utilisées

| Outil | Rôle |
|-------|------|
| **OpenAuto** | Système Android Auto pour Raspberry Pi |
| **Raspberry Pi OS** | Système de base |

---

##  Documentation

- [Installation](./installation.md) — Mise en place du système embarqué
- [Configuration](./configuration.md) — Paramétrage de l'interface et intégrations

---
