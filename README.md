# Aboone toi a ma chaine youtube : https://www.youtube.com/@Loic-Cybersecurite
# 🦾 Roomba WiFi Control avec ESP32 & Interface Web Joystick

## 🚀 Présentation

Ce projet permet de **contrôler un aspirateur Roomba (série 500/600/700...) via le WiFi avec un ESP32** et une **interface web joystick** (PC, tablette, smartphone).

**Fonctionnalités principales :**
- Déplacement en temps réel (joystick virtuel)
- Lecture du niveau de batterie
- Affichage des capteurs (pare-chocs, falaise…)
- Activation/désactivation des brosses
- 100% open-source, facilement modifiable

---

## 🛠️ Matériel nécessaire

- **ESP32** (ex : DevKit v1)
- **Roomba** compatible Open Interface (série 500/600/700...)
- **Fils Dupont** (pour connexion série et GND)
- **PC** pour programmer l’ESP32 (IDE Arduino recommandé)
- **Réseau WiFi** 2.4 GHz

---

## 📡 Schéma de câblage

| ESP32 (par défaut) | Roomba          |  
|--------------------|-----------------|  
| TX (GPIO 17)       | RX Roomba       |  
| RX (GPIO 16)       | TX Roomba       |  
| GND                | GND Roomba      |  
| –                  | Pin 7 → GND     |  

> **Remarques :**
> - **Pin 7 (“Device Detect”) du Roomba** doit être reliée à GND pour activer l’Open Interface.
> - **N’alimentez pas l’ESP32 depuis le Roomba** : préférez l’USB.

---

## ⚡️ Installation

### 1. Préparer l’environnement

- Installer l’[IDE Arduino](https://www.arduino.cc/en/software)
- Ajouter le support ESP32 (Gestionnaire de cartes)
- Installer les bibliothèques :
  - [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
  - [AsyncTCP](https://github.com/me-no-dev/AsyncTCP)
  - [ArduinoJson](https://github.com/bblanchon/ArduinoJson)

---

### 2. Configuration & Téléversement

- Ouvrez le fichier `.ino` dans l’IDE Arduino.
- **Modifiez vos identifiants WiFi** :

```cpp
const char* ssid = "TON_WIFI";
const char* password = "TON_MDP_WIFI";
