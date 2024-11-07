To design a traffic light system using Arduino, you can follow the steps below, which include the circuit setup and the corresponding Arduino code.

## Components Required

- **Arduino Uno** (or any compatible board)
- **3 LEDs** (Red, Yellow, Green)
- **3 Resistors** (220 ohms)
- **Breadboard**
- **Jumper wires**

## Circuit Setup

1. **Insert the LEDs** into the breadboard:
    - Place the Red LED, Yellow LED, and Green LED in a row.
    - Connect the longer lead (anode) of each LED to a separate row on the breadboard.
2. **Connect Resistors**:
    - Connect a 220-ohm resistor from the shorter lead (cathode) of each LED to the ground rail on the breadboard.
3. **Wiring to Arduino**:
    - Connect the anode of the Red LED to pin 2 on the Arduino.
    - Connect the anode of the Yellow LED to pin 3 on the Arduino.
    - Connect the anode of the Green LED to pin 4 on the Arduino.
    - Connect all cathodes to ground.

Arduino Code
Here is a simple Arduino sketch that simulates a traffic light sequence:
// Define pin numbers for LEDs
const int redLED = 2;    // Red LED connected to pin 2
const int yellowLED = 3; // Yellow LED connected to pin 3
const int greenLED = 4;  // Green LED connected to pin 4

void setup() {
    // Set LED pins as output
    pinMode(redLED, OUTPUT);
    pinMode(yellowLED, OUTPUT);
    pinMode(greenLED, OUTPUT);
}

void loop() {
    // Red light on
    digitalWrite(redLED, HIGH);
    delay(3000); // Stay red for 3 seconds

    // Red and Yellow lights on
    digitalWrite(yellowLED, HIGH);
    delay(1000); // Stay red and yellow for 1 second

    // Green light on
    digitalWrite(redLED, LOW);     // Turn off red
    digitalWrite(yellowLED, LOW);  // Turn off yellow
    digitalWrite(greenLED, HIGH);  // Turn on green
    delay(3000); // Stay green for 3 seconds

    // Yellow light on
    digitalWrite(greenLED, LOW);   // Turn off green
    digitalWrite(yellowLED, HIGH);  // Turn on yellow
    delay(1000); // Stay yellow for 1 second

    // Reset all lights off before repeating
    digitalWrite(yellowLED, LOW);
}

## Explanation of Code

- The **setup()** function initializes the pins connected to the LEDs as outputs.
- The **loop()** function controls the sequence of lights:
    - The red light stays on for 3 seconds.
    - Both red and yellow lights are on for 1 second.
    - The green light is then activated for another 3 seconds.
    - Finally, the yellow light is turned on for 1 second before resetting.

This code will create a simple traffic light simulation using LEDs. You can upload this code to your Arduino using the Arduino IDE and observe how it mimics real traffic light behavior.