# Home Assistant — Configuration

Ce guide couvre les intégrations, les automatisations et la personnalisation de Home Assistant.

---

## 1. Ajouter des intégrations

```
Paramètres > Appareils et services > Ajouter une intégration
```

### Intégrations populaires

| Intégration | Description |
|-------------|-------------|
| **Philips Hue** | Éclairage connecté via le pont Hue |
| **Google Cast** | Chromecast et Google Home |
| **Météo** | Prévisions météo locales |
| **Sonoff/eWeLink** | Prises et interrupteurs connectés |

## 2. Automatisations

### Créer une automatisation via l'interface

```
Paramètres > Automatisations > ➕ Créer une automatisation
```

Structure d'une automatisation :

- **Déclencheur (Trigger)** : ce qui déclenche l'action (heure, état d'un capteur, etc.)
- **Condition (optionnel)** : filtre supplémentaire
- **Action** : ce qui se passe (allumer une lumière, envoyer une notification, etc.)

### Exemple en YAML

```yaml
# /config/automations.yaml
- alias: "Lumière salon au coucher du soleil"
  trigger:
    - platform: sun
      event: sunset
      offset: "-00:30:00"
  condition:
    - condition: state
      entity_id: group.famille
      state: "home"
  action:
    - service: light.turn_on
      target:
        entity_id: light.salon
      data:
        brightness: 180
        color_temp: 400
```

### Exemple : notification au retour à la maison

```yaml
- alias: "Notification retour maison"
  trigger:
    - platform: state
      entity_id: person.prenom
      to: "home"
  action:
    - service: notify.mobile_app_mon_telephone
      data:
        title: "Bienvenue !"
        message: "Vous êtes rentré à la maison."
```

---

## 3. Scripts

```yaml
# /config/scripts.yaml
bonsoir:
  alias: "Mode Bonsoir"
  sequence:
    - service: light.turn_on
      target:
        entity_id: light.salon
      data:
        brightness: 100
    - service: media_player.volume_set
      target:
        entity_id: media_player.salon
      data:
        volume_level: 0.3
```

---

## 4. Tableaux de bord (Dashboards)

### Créer un dashboard personnalisé

```
Vue d'ensemble > ⋮ > Modifier le tableau de bord
```

### Cartes utiles

| Carte | Usage |
|-------|-------|
| **Entités** | Afficher l'état de plusieurs appareils |
| **Thermomètre** | Température et humidité |
| **Historique** | Graphique de l'évolution d'une valeur |
| **Alarme** | Panel d'alarme de sécurité |

---

## 5. Accès à distance

### Via reverse proxy Nginx (gratuit)

Identique à la configuration du serveur multimédia. Utiliser le port `8123` comme destination du proxy.

---

## 6. Notifications mobiles

### Installer l'application Home Assistant

Disponible sur App Store et Google Play.

### Configurer les notifications push

```yaml
action:
  - service: notify.mobile_app_nom_du_telephone
    data:
      title: "Alerte"
      message: "La porte du garage est ouverte depuis 30 minutes."
```

---

## 7. Sauvegardes

### Sauvegarde automatique

```
Paramètres > Système > Sauvegardes > Planifier
```
