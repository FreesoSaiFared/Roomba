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
