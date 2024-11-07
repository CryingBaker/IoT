To create a smoke detection system using Arduino that activates a buzzer when smoke is detected, you can use the **MQ-2** gas sensor. Below is a detailed guide on the components required, circuit setup, and the Arduino code.

## Components Required

- **Arduino Uno** (or any compatible board)
- **MQ-2 Gas Sensor**
- **Buzzer**
- **Red LED** (optional for visual indication)
- **220-ohm resistor** (for the LED)
- **Breadboard**
- **Jumper wires**

## Circuit Setup

1. **Connect the MQ-2 Sensor**:
    - The MQ-2 sensor has four pins: VCC, GND, A0 (analog output), and D0 (digital output).
    - Connect the **VCC pin** to the 5V pin on the Arduino.
    - Connect the **GND pin** to the ground (GND) on the Arduino.
    - Connect the **A0 pin** to an analog pin on the Arduino (e.g., A0).
    - Optionally connect the **D0 pin** if you want to use digital output.
2. **Connect the Buzzer**:
    - Connect one terminal of the buzzer to a digital pin on the Arduino (e.g., pin 9).
    - Connect the other terminal of the buzzer to GND.
3. **Connect an LED** (optional):
    - Connect a red LED with its anode (longer leg) to a digital pin (e.g., pin 10) through a 220-ohm resistor.
    - Connect the cathode (shorter leg) of the LED to GND.

## Arduino Code

Here’s a sample code that reads from the MQ-2 sensor and activates a buzzer when smoke is detected:
// Define pin numbers
const int mq2Pin = A0;      // Analog pin connected to MQ-2 sensor
const int buzzerPin = 9;    // Digital pin connected to buzzer
const int ledPin = 10;      // Digital pin connected to LED

// Smoke threshold value
const int smokeThreshold = 400; // Adjust this value based on your calibration

void setup() {
    Serial.begin(9600);        // Start serial communication
    pinMode(buzzerPin, OUTPUT); // Set buzzer as output
    pinMode(ledPin, OUTPUT);    // Set LED as output
}

void loop() {
    int smokeLevel = analogRead(mq2Pin); // Read smoke level from MQ-2 sensor

    Serial.print("Smoke Level: ");
    Serial.println(smokeLevel); // Print smoke level to Serial Monitor

    // Check if smoke level exceeds threshold
    if (smokeLevel > smokeThreshold) {
        digitalWrite(buzzerPin, HIGH); // Turn on buzzer
        digitalWrite(ledPin, HIGH);     // Turn on LED
    } else {
        digitalWrite(buzzerPin, LOW);  // Turn off buzzer
        digitalWrite(ledPin, LOW);      // Turn off LED
    }

    delay(1000); // Wait for 1 second before next reading
}

​
Explanation of Code
The code initializes serial communication and sets up pins for the buzzer and LED.
In the loop() function, it continuously reads the analog value from the MQ-2 sensor.
If the smoke level exceeds a predefined threshold (400 in this case), it activates the buzzer and turns on an LED for visual indication. If not, both are turned off.
How to Use
Upload this code to your Arduino using the Arduino IDE.
Open the Serial Monitor (Ctrl + Shift + M) in the IDE to view real-time smoke level readings.
When smoke is detected above the threshold, you will hear the buzzer sound and see the LED light up.
This setup provides a simple and effective smoke detection system using an Arduino and an MQ-2 gas sensor. Adjustments can be made based on specific requirements or sensitivity levels.
