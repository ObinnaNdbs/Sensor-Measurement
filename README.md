# DHT-11: Digital Temperature and Humidity Sensor
 
# Overview of DHT11: 
The DHT11 is an entry-level digital temperature and humidity sensor renowned for its simplicity and affordability.This sensor can be easily interfaced with any micro-controller such as Arduino, Raspberry Pi etc… to measure humidity and temperature instantaneously. It employs a capacitive humidity sensor and a thermistor to gauge the ambient conditions. Additionally, it features an 8-bit microcontroller for serial data output. Despite its basic design, precise timing is crucial for data retrieval, with updates available approximately every two seconds.

# Components and Functionality:
The DHT11 comprises a capacitive humidity sensor, a thermistor, an 8-bit microcontroller, and a resistor for pull-up functionality.
The capacitive humidity sensor measures humidity by detecting capacitance changes.
The thermistor detects temperature variations by monitoring electrical resistance.
An 8-bit microcontroller processes sensor data and facilitates serial data transmission.
A pull-up resistor ensures stable data communication.

# Operation Principle:
The DHT11 sensor comprises a capacitive humidity sensing element and a thermistor for temperature detection. Within the humidity sensing component, two electrodes sandwich a moisture-holding substrate, acting as a dielectric, leading to changes in capacitance relative to humidity fluctuations. The integrated circuit (IC) processes these alterations in resistance, converting them into digital signals.
 
For temperature measurement, the sensor utilizes a Negative Temperature Coefficient (NTC) thermistor, characterized by a decrease in resistance with rising temperatures. To enhance sensitivity, semiconductor ceramics or polymers are commonly employed to construct the sensor, ensuring substantial resistance variations even with minimal temperature changes.
Data transmission relies on a single-bus format, with 8-bit segments for humidity and temperature readings, along with a checksum for data integrity. 

# Connection
Positive and negative are connected to 5v and ground and digital(data) pin is connected to any digital pin on the audrino board. 
It is a library based code, so first we need to install the library for dht sensor.
In the DHT sensor library open DHT tester and set pin number to the pin you put it on {#define DHTPIN 2}.

# Coding

// Example testing sketch for various DHT humidity/temperature sensors

// Written by ladyada, public domain

// REQUIRES the following Arduino libraries:

// - DHT Sensor Library: https://github.com/adafruit/DHT-sensor-library

// - Adafruit Unified Sensor Lib: https://github.com/adafruit/Adafruit_Sensor

#include "DHT.h"

#define DHTPIN 34     // Digital pin connected to the DHT sensor

// Feather HUZZAH ESP8266 note: use pins 3, 4, 5, 12, 13 or 14 --

// Pin 15 can work but DHT must be disconnected during program upload.

// Uncomment whatever type you're using!

#define DHTTYPE DHT11   // DHT 11

//#define DHTTYPE DHT22   // DHT 22  (AM2302), AM2321

//#define DHTTYPE DHT21   // DHT 21 (AM2301)

// Connect pin 1 (on the left) of the sensor to +5V

// NOTE: If using a board with 3.3V logic like an Arduino Due connect pin 1

// to 3.3V instead of 5V!

// Connect pin 2 of the sensor to whatever your DHTPIN is

// Connect pin 3 (on the right) of the sensor to GROUND (if your sensor has 3 pins)

// Connect pin 4 (on the right) of the sensor to GROUND and leave the pin 3 EMPTY (if your sensor has 4 pins)

// Connect a 10K resistor from pin 2 (data) to pin 1 (power) of the sensor

// Initialize DHT sensor.

// Note that older versions of this library took an optional third parameter to

// tweak the timings for faster processors.  This parameter is no longer needed

// as the current DHT reading algorithm adjusts itself to work on faster procs.

DHT dht(DHTPIN, DHTTYPE);

void setup() {

  Serial.begin(9600);
  
  Serial.println(F("DHTxx test!"));

  dht.begin();
  
}

void loop() {

  // Wait a few seconds between measurements.
  
  delay(2000);

  // Reading temperature or humidity takes about 250 milliseconds!
  
  // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
  
  float h = dht.readHumidity();
  
  // Read temperature as Celsius (the default)
  
  float t = dht.readTemperature();
  
  // Read temperature as Fahrenheit (isFahrenheit = true)
  
  float f = dht.readTemperature(true);

  // Check if any reads failed and exit early (to try again).
  
  if (isnan(h) || isnan(t) || isnan(f)) {
  
    Serial.println(F("Failed to read from DHT sensor!"));
    
    return;
  }

  // Compute heat index in Fahrenheit (the default)
  
  float hif = dht.computeHeatIndex(f, h);

  // Compute heat index in Celsius (isFahreheit = false)
  
  float hic = dht.computeHeatIndex(t, h, false);

  Serial.print(F("Humidity: "));

  Serial.print(h);
  
  Serial.print(F("%  Temperature: "));
  
  Serial.print(t);
  
  Serial.print(F("°C "));
  
  Serial.print(f);
  
  Serial.print(F("°F  Heat index: "));
  
  Serial.print(hic);
  
  Serial.print(F("°C "));
  
  Serial.print(hif);
  
  Serial.println(F("°F"));
}

# Setup
![image](https://github.com/ObinnaNdbs/Sensor-Measurement/assets/159606096/60c5bdbe-f8f9-4797-a18e-5c00eb9dfc8f)

![IMG_8985](https://github.com/ObinnaNdbs/Sensor-Measurement/assets/159606096/141b375a-9bf2-4c94-8f40-2415fd348edb)
