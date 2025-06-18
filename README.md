
🚀 Présentation
Ce projet permet de contrôler un aspirateur Roomba (série 500/600/700...) en WiFi via un ESP32,
avec une interface web joystick (compatible PC, tablette, smartphone) :

Déplacement en temps réel

Lecture de l’état de la batterie

Affichage des capteurs (pare-chocs, falaise…)

Activation/désactivation des brosses

100% open-source, facile à adapter à vos besoins.

🛠 Matériel nécessaire
1 x ESP32 (ex : DevKit v1)

1 x Roomba compatible Open Interface (séries 500/600/700...)

Fils Dupont (pour le branchement série et GND)

Un PC pour programmer l’ESP32 (Arduino IDE recommandé)

Connexion WiFi locale (2.4 GHz)

📡 Câblage
TX ESP32 (GPIO 17 par défaut) → RX Roomba

RX ESP32 (GPIO 16 par défaut) → TX Roomba

GND ESP32 → GND Roomba

Pin 7 Roomba (Device Detect) → GND (permet d’activer le mode “Open Interface”)

ESP32 alimenté par USB (ne pas alimenter par le Roomba lui-même pour éviter les soucis au boot)

⚡️ Installation
1. Installer les bibliothèques Arduino
ESPAsyncWebServer

AsyncTCP

ArduinoJson

(Dans l’IDE Arduino, menu : Outils > Gérer les bibliothèques)

2. Téléverse le code
Ouvre le fichier .ino (fourni dans ce repo)

Modifie la section :

cpp
Copier
Modifier
const char* ssid = "TON_WIFI";
const char* password = "TON_MDP_WIFI";
avec les identifiants de ton réseau WiFi.

Téléverse sur l’ESP32 via USB.

3. Récupère l’adresse IP
Ouvre le Moniteur Série Arduino à 115200 bauds.

Note l’IP affichée à la fin du boot.

4. Utilise l’interface
Depuis ton PC, tablette ou smartphone (connecté au même WiFi), ouvre l’adresse IP de l’ESP32 dans le navigateur.

Tu peux piloter le Roomba via le joystick, voir le niveau de batterie, activer/désactiver les brosses, et voir les capteurs en temps réel.

🕹 Fonctionnalités de la page web
Joystick virtuel : contrôle direction & vitesse du Roomba

Bouton “Brosses ON/OFF” : démarre ou arrête les brosses et l’aspirateur

Niveau de batterie : affiché et mis à jour toutes les 2 secondes

Capteurs pare-choc / falaise : statut en temps réel

Réactif sur mobile et desktop

💡 Tuto écrit — Étape par étape
1️⃣ Préparation
Installe l’IDE Arduino

Ajoute le support ESP32 (Menu Outils > Gestionnaire de cartes > “esp32 by Espressif Systems”)

2️⃣ Télécharge les bibliothèques
ESPAsyncWebServer, AsyncTCP, ArduinoJson (par le gestionnaire de bibliothèques Arduino)

3️⃣ Branchement ESP32 ↔ Roomba
TX ESP32 (GPIO17) → RX Roomba

RX ESP32 (GPIO16) → TX Roomba

GND ESP32 → GND Roomba

Pin 7 Roomba → GND

4️⃣ Configuration & Téléversement
Modifie dans le code les identifiants WiFi (ssid / password)

Téléverse le code sur l’ESP32 via USB

5️⃣ Connexion & Utilisation
Ouvre le Moniteur Série (115200 bauds)

Note l’IP locale affichée

Depuis ton navigateur, ouvre cette IP : tu obtiens la page de contrôle

Teste le joystick, active les brosses, observe la batterie et les capteurs

6️⃣ Dépannage / FAQ
Si la page ne s’affiche pas : vérifie le WiFi, la connexion du RX/TX/GND, ou la bonne vitesse série (115200 bauds).

Si le Roomba ne bouge pas : vérifie la pin 7 à GND, et que le robot est réveillé.

Si tu veux activer uniquement certaines brosses ou l’aspi : change la valeur de MOTORS_ON dans le code (voir doc Roomba OI).

