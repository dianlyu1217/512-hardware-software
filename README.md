Smart Plant Health Monitoring System

This system utilizes temperature, humidity, and light intensity sensors to monitor plant health. It displays real-time data and health indicators on an LCD, with a stepper motor adjusting the display based on the plant's condition.

<img width="1093" alt="截屏2024-01-16 18 28 54" src="https://github.com/dianlyu1217/514-hardware-software/assets/146486958/4a516c44-3955-4db5-8441-28487bc0dd36">




Sensor Device
1. Temperature Sensor (DS18B20)
  - Digital temperature sensor with a range of -55°C to +125°C.
  - Offers high accuracy (±0.5°C) over a wide temperature range.
  - Utilizes a one-wire interface for communication.
2. Humidity Sensor (DHT22)
  - Measures humidity range of 0-100% with 2-5% accuracy.
  - Also capable of measuring temperature (-40°C to 80°C) with an accuracy of ±0.5°C.
  - Digital signal output with a single-wire interface.
3. Light Intensity Sensor (BH1750)
  - Digital ambient light sensor providing illuminance measurements in lux.
  - Communicates over an I2C interface.
  - Wide range and high resolution.
![image](https://github.com/dianlyu1217/514-hardware-software/assets/146486958/1862f83d-e6a8-4bfa-9244-9ba8aef1f511)


Display Device
1. LCD Display (16x2 Character LCD)
  - A 16x2 character LCD screen to display real-time data (temperature, humidity, light intensity) and plant health status.
  - Backlit for clear visibility in various lighting conditions.
  - Interface: Parallel or I2C for communication with the microcontroller.
2. Stepper Motor (NEMA 17) with Driver (A4988)
  - NEMA 17 stepper motor is used to adjust the display's position or an indicator based on the plant's health.
  - The A4988 driver allows precise control of the motor's steps and direction.
  - Integration with the Arduino for responsive adjustments according to the sensor readings.

![image](https://github.com/dianlyu1217/514-hardware-software/assets/146486958/ef5413a6-4e63-4114-9bee-7dcfe16c4281)


Communication between Devices
![image](https://github.com/dianlyu1217/514-hardware-software/assets/146486958/9bc1bef9-d57f-4ead-b482-bf24ffda68d4)
1. Data Collection
  - The temperature, humidity, and light intensity sensors collect environmental data around the plant.
  - Each sensor sends its data to the microcontroller (Arduino UNO) using appropriate communication protocols (One-wire for DS18B20, single-wire for DHT22, and I2C for BH1750).
2. Data Processing
  - The Arduino UNO acts as the central processing unit.
  - It reads and processes the data received from all the sensors.
  - Determines the health status of the plant based on pre-defined thresholds and algorithms.
3. Data Display and Indication
  - Processed data and health status are displayed on the LCD screen.
  - The stepper motor, controlled by the Arduino through the A4988 driver, adjusts the position of an indicator or the display itself based on the plant's health.
4. Power Management
  - A power module (LM2596) ensures stable power supply to all components.
  - Proper voltage levels are maintained for sensors, Arduino, display, and motor. 
