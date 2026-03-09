#  Home Assistant — Installation

---

##  1. Home Assistant OS 

Home Assistant OS est une image système complète dédiée. Elle inclut le superviseur HA et les add-ons.

### 1.1 Télécharger l'image

Télécharger l'image officielle pour Raspberry Pi 4 :
 [https://www.home-assistant.io/installation/raspberrypi](https://www.home-assistant.io/installation/raspberrypi)

### 1.2 Flasher la carte SD

Utiliser **Raspberry Pi Imager** :

```
Raspberry Pi Imager > Choisir un OS > Utiliser une image personnalisée > sélectionner le fichier .img.xz
```

### 1.3 Démarrer le Raspberry Pi

1. Insérer la carte SD dans le Raspberry Pi
2. Connecter le câble Ethernet (recommandé pour la première installation)
3. Brancher l'alimentation
4. Attendre 5 à 10 minutes pour le premier démarrage

### 1.4 Accéder à l'interface web

Ouvrir dans un navigateur :

```
http://homeassistant.local:8123
```

Ou via l'IP du Raspberry Pi :

```
http://192.168.1.X:8123
```

---

## 2. Configuration initiale

### 2.1 Créer le compte administrateur

1. Sur la page d'accueil : **Créer mon compte **
2. Renseigner : nom, identifiant, mot de passe
3. Configurer la localisation (fuseau horaire, coordonnées GPS)
4. Choisir les unités (métrique)
5. Valider la découverte automatique des appareils détectés

### 2.2 Configurer une IP statique 

```
Paramètres > Système > Réseau > Modifier l'interface réseau
```

Définir une adresse IP fixe pour le Raspberry Pi.

---

## 3. Mise à jour

```
Paramètres > Système > Mises à jour
```

##  Résumé

| Service | Port |
|---------|------|
| Interface web Home Assistant | 8123 |
| Home Assistant API | 8123 |
