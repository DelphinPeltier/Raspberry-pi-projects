#  Android Auto — Configuration

Ce guide couvre la configuration du système embarqué, l'optimisation des performances et les ajustements pour l'usage en voiture.

---

## 1. Configuration audio

### Sortie audio via jack 3.5mm

```bash
sudo raspi-config
# System Options > Audio > Headphones
```

### Sortie audio via carte son USB

```bash
# Lister les périphériques audio
aplay -l

# Définir la carte USB comme sortie par défaut
sudo nano /etc/asound.conf
```

```
pcm.!default {
    type hw
    card 1      # Numéro de la carte USB
}
ctl.!default {
    type hw
    card 1
}
```

---

## 2. Optimisation des performances

### Désactiver les services inutiles

```bash
# Désactiver Bluetooth si non utilisé
sudo systemctl disable bluetooth

# Désactiver le Wi-Fi si connexion filaire uniquement
sudo systemctl disable wpa_supplicant
```

### Optimiser la mémoire GPU

```bash
sudo nano /boot/config.txt
```

```ini
gpu_mem=256   # Allouer plus de mémoire GPU pour l'affichage
```

---

## 3. Démarrage rapide

### Désactiver le splash screen

```bash
sudo nano /boot/cmdline.txt
```

Supprimer `splash` et `quiet` si présents, ajouter :

```
fastboot noswap
```

### Réduire le délai de démarrage systemd

```bash
sudo nano /etc/systemd/system.conf
```

```ini
DefaultTimeoutStartSec=10s
DefaultTimeoutStopSec=10s
```

---

## 4. Configuration Android Auto (côté smartphone)

### Activer Android Auto en mode filaire

Sur le smartphone Android :

1. Aller dans **Paramètres > Applications > Android Auto**
2. Activer le mode développeur (appui prolongé sur le numéro de version)
3. Activer **Unknown sources** dans les paramètres développeur Android Auto

### Android Auto Wireless (sans fil)

Nécessite un adaptateur Wi-Fi 5 GHz sur le Raspberry Pi :

```bash
sudo apt install hostapd dnsmasq -y
```

Configurer un hotspot Wi-Fi dédié à la connexion Android Auto sans fil.

---

## 5. Paramètres d'affichage

### Résolution écran

```bash
sudo nano /boot/config.txt
```

```ini
hdmi_group=2
hdmi_mode=87
hdmi_cvt=1024 600 60 6 0 0 0   # Pour un écran 7" 1024x600
```

### Désactiver l'économiseur d'écran

```bash
sudo nano /etc/lightdm/lightdm.conf
```

```ini
[Seat:*]
xserver-command=X -s 0 -dpms
```

---

## 6. Gestion de l'alimentation

### Script d'arrêt propre au coupé-contact

Brancher un fil depuis l'accessoire (ACC) du véhicule vers un GPIO du Raspberry Pi via un résistance et un optocoupleur.

Script d'arrêt :

```bash
nano ~/scripts/shutdown-monitor.py
```

```python
import RPi.GPIO as GPIO
import subprocess
import time

ACC_PIN = 17  # GPIO 17

GPIO.setmode(GPIO.BCM)
GPIO.setup(ACC_PIN, GPIO.IN, pull_up_down=GPIO.PUD_UP)

while True:
    if GPIO.input(ACC_PIN) == GPIO.LOW:
        # ACC coupé, attendre 3 secondes puis éteindre
        time.sleep(3)
        if GPIO.input(ACC_PIN) == GPIO.LOW:
            subprocess.call(['sudo', 'shutdown', '-h', 'now'])
    time.sleep(1)
```

Lancer au démarrage via crontab :

```bash
crontab -e
```

```
@reboot python3 /home/pi/scripts/shutdown-monitor.py &
```

---
