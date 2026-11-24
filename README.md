# iot
🌱 IoT-Based Smart Agriculture Monitoring System
An IoT-based automatic irrigation and environmental monitoring system using ESP8266, DHT22, a soil moisture sensor, OLED display, relay, and ThingSpeak Cloud.

📌 Project Overview
The IoT-Based Smart Agriculture Monitoring System monitors soil moisture, temperature, and humidity in real time and automatically controls irrigation based on soil moisture conditions.

The system uses an ESP8266 NodeMCU as its main controller. A soil moisture sensor measures the water content in the soil, while a DHT22 sensor measures ambient temperature and humidity. The readings are displayed on a 128×64 OLED display.

When the smoothed soil moisture percentage falls below 30%, the ESP8266 activates a relay-controlled water pump. When the moisture level reaches 30% or above, the pump is switched off. Sensor readings are also uploaded to the ThingSpeak Cloud Platform over Wi-Fi every 15 seconds for remote monitoring.

🎯 Objectives
Monitor soil moisture continuously.
Measure environmental temperature and humidity.
Automatically switch the irrigation pump ON or OFF.
Display sensor readings and pump status on an OLED display.
Upload sensor data to ThingSpeak for remote monitoring.
Reduce unnecessary water use and manual monitoring.
🛠️ Hardware Components
No.	Component	Function
1	ESP8266 NodeMCU	Main controller and Wi-Fi communication
2	Soil moisture sensor	Measures soil moisture
3	DHT22 sensor	Measures temperature and humidity
4	OLED display (128×64)	Displays sensor readings
5	Relay module	Switches the water pump
6	DC water pump	Supplies water for irrigation
7	Red LED	Indicates temperature above 30°C
8	Green LED	Indicates temperature at or below 30°C
9	Jumper wires	Electrical connections
10	Power supply	Powers the circuit
🔌 Pin Connections
Component	ESP8266 NodeMCU Pin
DHT22 data	D4
OLED SDA	D2
OLED SCL	D1
Soil moisture analog output	A0
Red LED	D5
Green LED	D6
Relay input	D7
OLED I²C address: 0x3C
