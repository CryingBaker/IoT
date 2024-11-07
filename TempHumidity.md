To print temperature and humidity readings on the Serial Monitor using an appropriate sensor, you can use the **DHT11** or **DHT22** sensor, which are popular for measuring temperature and humidity. Below are the steps for setting up the circuit and the corresponding Arduino code.

## Components Required

- **Arduino Uno** (or any compatible board)
- **DHT11 or DHT22 Sensor**
- **10k ohm resistor** (only for DHT22)
- **Breadboard**
- **Jumper wires**

## Circuit Setup

1. **Connect the DHT Sensor**:
    - The DHT sensor has three pins: VCC, GND, and DATA.
    - Connect the **VCC pin** to the 5V pin on the Arduino.
    - Connect the **GND pin** to the ground (GND) on the Arduino.
    - Connect the **DATA pin** to a digital pin on the Arduino (e.g., pin 7).
2. **Add a Pull-Up Resistor** (for DHT22):
    - If you are using a DHT22 sensor, connect a 10k ohm resistor between the VCC and DATA pins.

You will need to install the **DHT sensor library** to interface with the sensor. You can do this via the Library Manager in the Arduino IDE by searching for "DHT sensor library" by Adafruit.

Here is a sample code to read temperature and humidity from the DHT sensor and print it to the Serial Monitor:
#include <DHT.h>

// Define DHT sensor type and pin
#define DHTTYPE DHT11 // Change to DHT22 if using that model
#define DHTPIN 7      // Pin where the data line is connected

// Create an instance of the DHT class
DHT dht(DHTPIN, DHTTYPE);

void setup() {
    // Start serial communication at 9600 baud rate
    Serial.begin(9600);
    // Initialize the DHT sensor
    dht.begin();
}

void loop() {
    // Wait a few seconds between measurements
    delay(2000);

    // Read temperature as Celsius
    float temperature = dht.readTemperature();
    // Read humidity
    float humidity = dht.readHumidity();

    // Check if any reads failed and exit early (to try again).
    if (isnan(temperature) || isnan(humidity)) {
        Serial.println("Failed to read from DHT sensor!");
        return;
    }

    // Print temperature and humidity to Serial Monitor
    Serial.print("Temperature: ");
    Serial.print(temperature);
    Serial.print(" °C");
    Serial.print("\\tHumidity: ");
    Serial.print(humidity);
    Serial.println(" %");
}

​
Explanation of Code
The code includes the DHT library, which provides functions for interacting with DHT sensors.
In setup(), serial communication is initiated, and the DHT sensor is initialized.
The loop() function waits for 2 seconds between readings, retrieves temperature and humidity data, checks for errors, and prints the values to the Serial Monitor.
How to Use
Upload this code to your Arduino using the Arduino IDE.
Open the Serial Monitor (Ctrl + Shift + M) in the IDE.
Set it to 9600 baud rate to match your code's settings.
You should see continuous readings of temperature and humidity printed every 2 seconds.
This setup allows you to monitor environmental conditions easily using an Arduino and a DHT sensor.