# C3-Mini Sensor SHT40 Piggyback

![image alt](https://github.com/0mollo/C3-Mini-Sensor-SHT40-Piggyback/blob/main/SHT%2040%20Piggyback%20top%20view.png) | ![image alt](https://github.com/0mollo/C3-Mini-Sensor-SHT40-Piggyback/blob/main/SHT%2040%20Piggyback%20bottom%20view.png?raw=true)

Temperature & Relative Humidity Module  
Version: V1.3  


##  Overview

The C3-Mini SHT40 Piggyback is a precision environmental sensing module designed for seamless stacking onto the Carenuity C3-Mini development board.

It enables:

- High-accuracy temperature measurement
- Precision relative humidity sensing
- Climate monitoring
- Indoor air condition analysis
- Environmental data logging

Built around the Sensirion SHT40 digital sensor.


##  Technical Specifications

| Parameter | Value |
|------------|--------|
| Sensor | Sensirion SHT40 |
| Interface | I2C |
| Operating Voltage | 3.3V |
| Logic Level | 3.3V |
| Temperature Range | -40°C to +125°C |
| Humidity Range | 0 – 100 %RH |
| Temperature Accuracy | ±0.2°C |
| Humidity Accuracy | ±1.8 %RH |
| Typical Current | 0.4 mA |


##  Sensor Header Pinout

| Pin | Function |
|------|----------|
| VIN | 3.3V |
| GND | Ground |
| SCL | I2C Clock |
| SDA | I2C Data |


##  C3-Mini GPIO Mapping

Recommended I2C configuration:

| C3-Mini Pin | SHT40 |
|-------------|--------|
| GPIO8 | SDA |
| GPIO10 | SCL |
| 3V3 | VIN |
| GND | GND |

## Board Schematic

[See](https://github.com/0mollo/C3-Mini-Sensor-SHT40-Piggyback/blob/main/SHT%2040%20Piggyback.pdf)

##  Board Dimensions

- Designed to match Carenuity C3-Mini piggyback footprint
- Compact vertical stack design
- Version marking: V1.3

 ## Associated Libraries

[Adafruit SHT4x Library](https://docs.arduino.cc/libraries/adafruit-sht4x-library/)
[Adafruit Unified Sensor](https://docs.arduino.cc/libraries/adafruit-unified-sensor/)

## Arduino Example Code

```cpp
#include <Wire.h>
#include <Adafruit_SHT4x.h>

Adafruit_SHT4x sht4 = Adafruit_SHT4x();

void setup() {
  Serial.begin(115200);
  Wire.begin(8, 10); // SDA, SCL for C3 Mini

  if (!sht4.begin()) {
    Serial.println("Couldn't find SHT40");
    while (1);
  }

  Serial.println("SHT40 detected");
}

void loop() {
  sensors_event_t humidity, temp;
  sht4.getEvent(&humidity, &temp);

  Serial.print("Temperature: ");
  Serial.print(temp.temperature);
  Serial.println(" °C");

  Serial.print("Humidity: ");
  Serial.print(humidity.relative_humidity);
  Serial.println(" %RH");

  Serial.println();
  delay(2000);
}
