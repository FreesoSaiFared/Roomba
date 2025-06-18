
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



