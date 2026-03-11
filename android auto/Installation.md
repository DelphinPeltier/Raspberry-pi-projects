#  Android Auto — Installation

Ce guide décrit l'installation d'un système Android Auto sur Raspberry Pi.

---

## 1. Installation manuelle sur Raspberry Pi OS

### 1.1 Prérequis système

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y \
  cmake build-essential \
  libboost-all-dev \
  libusb-1.0-0-dev \
  libssl-dev \
  libprotobuf-dev \
  protobuf-compiler \
  librtaudio-dev \
  libpulse-dev \
  libgstreamer1.0-dev \
  gstreamer1.0-plugins-base \
  gstreamer1.0-plugins-good \
  qt5-default \
  libqt5multimedia5-plugins
```

### 1.2 Compiler OpenAuto

```bash
git clone https://github.com/f1xpl/openauto.git
cd openauto
mkdir build && cd build
cmake ..
make -j4
```

---

## 2. Configuration de l'écran tactile

### Rotation de l'écran 

```bash
sudo nano /boot/config.txt
```

Ajouter :

```
display_rotate=1    # 90° (paysage inversé)
# display_rotate=2  # 180°
# display_rotate=3  # 270°
```

### Calibration tactile

```bash
sudo apt install xinput-calibrator -y
xinput_calibrator
```

---

## 3. Démarrage automatique

Pour lancer automatiquement l'interface au démarrage, configurer un autostart :

```bash
mkdir -p ~/.config/autostart
nano ~/.config/autostart/openauto.desktop
```

```ini
[Desktop Entry]
Type=Application
Name=OpenAuto
Exec=/chemin/vers/openauto
```

---

## 4. Alimentation dans le véhicule

### Schéma de connexion simplifié

```
Batterie 12V → Fusible 5A → Convertisseur DC-DC 12V→5V 3A → Raspberry Pi (USB-C)
```

### Arrêt propre au coupé-contact

Utiliser un module d'alimentation intelligent PiJuice pour gérer l'arrêt propre du système quand le contact est coupé.

---

##  Résumé

| Composant | Connexion |
|-----------|-----------|
| Écran | HDMI + USB (tactile) |
| Smartphone | USB-A port du Pi |
| Audio | Jack 3.5mm  |
| Alimentation | Convertisseur 12V → USB-C |
