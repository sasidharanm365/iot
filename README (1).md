# 🌱 IoT-Based Smart Agriculture Monitoring System

**An IoT-based automatic irrigation and environmental monitoring system using ESP8266, DHT22, a soil moisture sensor, OLED display, relay, and ThingSpeak Cloud.**

## 📌 Project Overview

The IoT-Based Smart Agriculture Monitoring System monitors soil moisture, temperature, and humidity in real time and automatically controls irrigation based on soil moisture conditions.

The system uses an **ESP8266 NodeMCU** as its main controller. A soil moisture sensor measures the water content in the soil, while a DHT22 sensor measures ambient temperature and humidity. The readings are displayed on a 128×64 OLED display.

When the smoothed soil moisture percentage falls below 30%, the ESP8266 activates a relay-controlled water pump. When the moisture level reaches 30% or above, the pump is switched off. Sensor readings are also uploaded to the **ThingSpeak Cloud Platform** over Wi-Fi every 15 seconds for remote monitoring.

## 🎯 Objectives

- Monitor soil moisture continuously.
- Measure environmental temperature and humidity.
- Automatically switch the irrigation pump ON or OFF.
- Display sensor readings and pump status on an OLED display.
- Upload sensor data to ThingSpeak for remote monitoring.
- Reduce unnecessary water use and manual monitoring.

## 🛠️ Hardware Components

| No. | Component | Function |
|---|---|---|
| 1 | ESP8266 NodeMCU | Main controller and Wi-Fi communication |
| 2 | Soil moisture sensor | Measures soil moisture |
| 3 | DHT22 sensor | Measures temperature and humidity |
| 4 | OLED display (128×64) | Displays sensor readings |
| 5 | Relay module | Switches the water pump |
| 6 | DC water pump | Supplies water for irrigation |
| 7 | Red LED | Indicates temperature above 30°C |
| 8 | Green LED | Indicates temperature at or below 30°C |
| 9 | Jumper wires | Electrical connections |
| 10 | Power supply | Powers the circuit |

## 🔌 Pin Connections

| Component | ESP8266 NodeMCU Pin |
|---|---|
| DHT22 data | D4 |
| OLED SDA | D2 |
| OLED SCL | D1 |
| Soil moisture analog output | A0 |
| Red LED | D5 |
| Green LED | D6 |
| Relay input | D7 |

**OLED I²C address:** `0x3C`

## 💻 Software and Libraries

- Arduino IDE
- Arduino C/C++
- ESP8266 board package
- Adafruit GFX Library
- Adafruit SSD1306 Library
- DHT Sensor Library (Adafruit)
- Wire library
- ESP8266WiFi library (included with the ESP8266 board package)

## ⚙️ Working Principle

1. On startup, the ESP8266 initializes the relay, LEDs, I²C interface, DHT22 sensor, and OLED display.
2. The ESP8266 connects to the configured Wi-Fi network.
3. The DHT22 measures temperature and humidity.
4. The soil moisture sensor provides an analog reading through pin A0.
5. The program converts the raw soil reading into a percentage using the configured dry and wet calibration values.
6. Exponential smoothing is applied to the soil moisture percentage to reduce sudden variations.
7. If the smoothed soil moisture is below 30%, the relay is activated and the water pump turns ON.
8. If the smoothed soil moisture is 30% or above, the relay is deactivated and the pump turns OFF.
9. The red LED turns ON when temperature is above 30°C. Otherwise, the green LED turns ON.
10. Temperature, humidity, soil moisture, and pump status are shown on the OLED display.
11. The three sensor readings are sent to ThingSpeak every 15 seconds.

## 📐 Soil Moisture Calculation

The program uses these calibration values:

- Dry soil value: `890`
- Wet soil value: `520`

The soil moisture percentage is calculated as:

```text
Soil Moisture (%) =
((DRY_VALUE - Soil_Raw) / (DRY_VALUE - WET_VALUE)) × 100
```

The result is constrained to a range of 0% to 100%.

### Soil Moisture Smoothing

The code uses the following smoothing equation:

```text
Smoothed Soil = (0.7 × Previous Smoothed Soil)
              + (0.3 × Current Soil Percentage)
```

## 🔄 Control Logic

| Condition | System response |
|---|---|
| Smoothed soil moisture below 30% | Pump ON |
| Smoothed soil moisture 30% or above | Pump OFF |
| Temperature above 30°C | Red LED ON, green LED OFF |
| Temperature at or below 30°C | Red LED OFF, green LED ON |
| DHT22 temperature or humidity reading fails | Relay set to OFF and sensor error shown |

**Relay note:** The supplied program uses an active-LOW relay: `LOW` means ON and `HIGH` means OFF.

## ☁️ ThingSpeak Cloud Monitoring

ThingSpeak is used to receive, store, and visualize sensor readings.

| ThingSpeak field | Data |
|---|---|
| Field 1 | Temperature (°C) |
| Field 2 | Humidity (%) |
| Field 3 | Soil moisture (%) |

The ESP8266 sends HTTP GET requests to the ThingSpeak update endpoint. The configured upload interval is 15 seconds.

Website: https://thingspeak.mathworks.com/

## 🖥️ OLED Display

The OLED display shows:

- Temperature in °C
- Relative humidity in %
- Soil moisture in %
- Water pump status (ON/OFF)

## 🚀 Setup and Installation

1. Install the [Arduino IDE](https://www.arduino.cc/en/software).
2. Install ESP8266 board support using Boards Manager.
3. Install the Adafruit GFX, Adafruit SSD1306, and DHT Sensor libraries.
4. Connect the components using the pin configuration in this README.
5. Open the Arduino sketch in the `Code` folder.
6. Enter your own Wi-Fi credentials and ThingSpeak Write API Key in the sketch.
7. Select **NodeMCU 1.0 (ESP-12E Module)** and the correct COM port.
8. Upload the sketch to the ESP8266.
9. Open the ThingSpeak channel dashboard to view the uploaded readings.

### Credentials

Before publishing the source code, replace all private credentials with placeholders:

```cpp
const char* ssid = "YOUR_WIFI_NAME";
const char* password = "YOUR_WIFI_PASSWORD";

String apiKey = "YOUR_THINGSPEAK_WRITE_API_KEY";
```

Enter the real values locally in your Arduino sketch. **Never commit Wi-Fi passwords or private API keys to a public repository.** If real credentials have already been published, change the Wi-Fi password and regenerate the ThingSpeak Write API Key.

## 📁 Suggested Repository Structure

```text
iot-based-smart-agriculture-monitoring-system/
├── README.md
├── Code/
│   └── smart_agriculture.ino
├── Circuit_Diagram/
│   └── circuit_diagram.png
├── Images/
│   ├── prototype.jpg
│   └── oled_display.jpg
├── Documentation/
│   └── IOT_REPORT.pdf
└── LICENSE
```

Add your actual circuit diagram, prototype photographs, and project report to the relevant folders. The filenames above are suggested names.

## 🌟 Advantages

- Automatic irrigation based on soil moisture.
- Reduced unnecessary water consumption.
- Real-time temperature, humidity, and soil moisture monitoring.
- Remote sensor-data visualization through ThingSpeak.
- Reduced need for continuous manual inspection.
- Simple and low-cost prototype suitable for educational use.

## 🔮 Future Scope

- Integrate weather forecast data to help avoid irrigation before expected rainfall.
- Develop a mobile application for monitoring and control.
- Use machine learning to estimate crop water requirements.
- Add solar power and battery backup.
- Extend the system to multiple irrigation zones.
- Add alerts for abnormal sensor readings and low soil moisture.

## 🌾 Applications

- Smart agriculture and precision farming
- Automatic irrigation
- Greenhouse monitoring
- Garden and plant monitoring
- Agricultural research
- IoT-based environmental monitoring

## 👨‍💻 Project Team

**Project:** IoT-Based Smart Agriculture Monitoring System  
**Course:** ECC1295 – IoT in Robotics  
**Department:** Electronics and Communication Engineering  
**Institution:** K. Ramakrishnan College of Engineering (Autonomous), Samayapuram, Trichy  
**Project Guide:** Mrs. R. Ramya, M.Tech., (Ph.D.)

**Team Members**
- S. Niranjan
- M. Pranav
- M. Sasi Dharan
- S. Vishnu Prasath

## 📜 License

This project is intended for educational, academic, and research purposes. Add a specific open-source license file if you want to grant reuse and redistribution permissions.

---

<p align="center">
  <strong>🌱 Smart Agriculture | IoT | ESP8266 | Automatic Irrigation | ThingSpeak</strong><br>
  <em>Making Agriculture Smarter Through IoT Technology.</em>
</p>
