Translated from the French source (video in French). 

This [Reddit thread](https://www.reddit.com/r/esp32/comments/1lfj48y/i_modified_my_roomba_using_an_esp32/) reported on it. There was an [attempt](https://github.com/Wummeke/Roomba-ESP8266-MQTT) years ago,  but that stranded on not being able to wake up from the docking state. This is apparently not a problem according to this new implementation: 

##### Have you find a solution to the wake from dock issue? I played with this years ago, but back then no one was able to wake the Roomba reliable, when it is docked. See [this repo on GitHub ](https://github.com/Wummeke/Roomba-ESP8266-MQTT) ⏤ by *wummeke* (↑ 2/ ↓ 0)
├─ I had this issue once. I had to remove the battery for about 20 seconds, and it never happened again. ⏤ by *TallReflection1263* (↑ 2/ ↓ 0)
└────

# Possible caveat for the newer models (might not work)
##### I wonder if this works with the new more basic models. Probably they don't have that dev port anymore. ⏤ by *Alienhaslanded* (↑ 1/ ↓ 0)
├─ I don’t think so :/ ⏤ by *TallReflection1263* (↑ 1/ ↓ 0)
└────


# Control a Roomba over WiFi with an ESP32 and a Web Interface

This guide explains how to take control of your Roomba vacuum (500/600/700 series) using an ESP32 board, all driven by a web interface accessible from your phone, tablet, or computer.

**Associated YouTube Channel:** [Loic Cybersecurite](https://www.youtube.com/@Loic-Cybersecurite)

---

## 🚀 Project Features

* **Real-time Control:** Drive your Roomba with a virtual joystick.
* **Status Monitoring:** Check the battery level in real-time.
* **Sensor Data:** View feedback from sensors (bumpers, cliffs, etc.).
* **Brush Control:** Toggle the cleaning brushes on demand.
* **Open-Source:** The project is fully open-source and easy to modify to fit your needs.

---

## 🛠️ Required Hardware

To build this project, you will need the following components:

* An **ESP32** development board (e.g., a DevKit v1 model).
* A **Roomba** compatible with the Open Interface (typically 500, 600, or 700 series).
* A few **Dupont jumper wires** (male/female) for the connections.
* A **computer** to program the ESP32 using the Arduino IDE.
* A **2.4 GHz WiFi network**.

---

## 📡 Wiring Diagram

The connection between the ESP32 and the Roomba's serial port is straightforward. Follow the table below:

| ESP32 (Default Pins) | Roomba (Mini-DIN Port) |
| :------------------- | :--------------------- |
| **GND** | GND                    |
| **TX (GPIO 17)** | Roomba RX              |
| **RX (GPIO 16)** | Roomba TX              |
| *Not Connected* | Pin 7 ("Device Detect") → **GND** |

> **⚠️ Important Notes:**
>
> 1.  To enable the Roomba's "Open Interface" mode, its **Pin 7 ("Device Detect") must be connected to ground (GND)**.
> 2.  Do not attempt to power the ESP32 from the Roomba. Use a stable, external power source like your computer's **USB port** or a wall adapter.

---

## ⚡️ Software Setup Guide

### 1. Preparing the Development Environment

1.  **Install the Arduino IDE:** If you haven't already, download and install the software from the [official Arduino website](https://www.arduino.cc/en/software).
2.  **Add ESP32 Board Support:** In the IDE, go to `File > Preferences` and add the following URL to the "Additional Boards Manager URLs" field: `https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json`. Then, install `esp32` from `Tools > Board > Boards Manager`.
3.  **Install the Required Libraries:** Using the Library Manager (`Sketch > Include Library > Manage Libraries...`), search for and install the following:
    * `ESPAsyncWebServer`
    * `AsyncTCP`
    * `ArduinoJson`

### 2. Configuration and Uploading

1.  Open the project file (`.ino`) in your Arduino IDE.
2.  Find and modify the following lines to enter your WiFi credentials:

```cpp
// --- Edit your WiFi credentials here ---
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
```

3.  Connect your ESP32 to your computer, select the correct COM port and board type (e.g., `DOIT ESP32 DEVKIT V1`) from the `Tools` menu.
4.  Click the **Upload** button to compile and flash the program onto the ESP32.

Once the upload is complete, the ESP32 will connect to your WiFi. You can then access the control interface via the IP address displayed in the Serial Monitor.




# Roomba-ESP8266-MQTT

From: https://github.com/Wummeke/Roomba-ESP8266-MQTT

Code, hints, tips, tricks and general documentation used as basis and lots of inspiration (in non particular order):
* https://github.com/thehookup/MQTT-Roomba-ESP01
* https://github.com/Mjrovai/Roomba_BT_Ctrl
* https://github.com/johnboiles/esp-roomba-mqtt
* https://www.bakke.online/index.php/2017/06/02/self-updating-ota-firmware-for-esp8266/
* https://forum.mysensors.org/post/52800
* http://anrg.usc.edu/ee579/spring2016/Roomba/iRobot_Roomba_600_Open_Interface_Spec.pdf

Uses Roomba library by Mike Macauley:
* http://www.airspayce.com/mikem/arduino/Roomba

# wiring:

```
Roomba  ESP
-----------
RX      TX
VCC     VCC
GND     GND
BRC     GPIO0
TX      RX
```
Note, I amplified  the TX signal from the Roomba with PNP transistor. See documentation in the Roomba library mentioned above and/or wiring scheme in the Hook Up's repository. This is different from John Boiles solution, who uses a voltage devider to lower the voltage of the TX signal. Not sure which approach is better, but using the transistor works fine for me.

# known issue:
My Roomba 650 won't wake up from sleep when docked. Tried pulsing BRC-pin low every 28 secs, but  Roomba resets itself after an hour or so. After that it won't wakeup unless I press the Clean button. However, it still responds with status information every so much minutes. 

If anyone has a sollution to this issue... Please let me know!



