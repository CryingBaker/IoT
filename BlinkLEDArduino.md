To blink four LEDs one by one with a 3-second delay using an Arduino, you can follow the instructions below, which include the circuit setup and the corresponding Arduino code.

## Components Required

- **Arduino Uno** (or any compatible board)
- **4 LEDs** (e.g., Red, Green, Blue, Yellow)
- **4 Resistors** (220 ohms for each LED)
- **Breadboard**
- **Jumper wires**

## Circuit Setup

1. **Insert the LEDs** into the breadboard:
    - Place the four LEDs in a row.
    - Connect the longer lead (anode) of each LED to a separate row on the breadboard.
2. **Connect Resistors**:
    - Connect a 220-ohm resistor from the shorter lead (cathode) of each LED to the ground rail on the breadboard.
3. **Wiring to Arduino**:
    - Connect the anode of the Red LED to pin 2 on the Arduino.
    - Connect the anode of the Green LED to pin 3 on the Arduino.
    - Connect the anode of the Blue LED to pin 4 on the Arduino.
    - Connect the anode of the Yellow LED to pin 5 on the Arduino.
    - Connect all cathodes to ground.

Arduino Code
Here is a simple code that will blink four LEDs one by one with a 3-second delay:
```cpp
// Define pin numbers for LEDs
const int redLED = 2;    // Red LED connected to pin 2
const int greenLED = 3;  // Green LED connected to pin 3
const int blueLED = 4;   // Blue LED connected to pin 4
const int yellowLED = 5; // Yellow LED connected to pin 5

void setup() {
    // Set LED pins as output
    pinMode(redLED, OUTPUT);
    pinMode(greenLED, OUTPUT);
    pinMode(blueLED, OUTPUT);
    pinMode(yellowLED, OUTPUT);
}

void loop() {
    // Turn on Red LED
    digitalWrite(redLED, HIGH);
    delay(3000); // Wait for 3 seconds
    digitalWrite(redLED, LOW); // Turn off Red LED

    // Turn on Green LED
    digitalWrite(greenLED, HIGH);
    delay(3000); // Wait for 3 seconds
    digitalWrite(greenLED, LOW); // Turn off Green LED

    // Turn on Blue LED
    digitalWrite(blueLED, HIGH);
    delay(3000); // Wait for 3 seconds
    digitalWrite(blueLED, LOW); // Turn off Blue LED

    // Turn on Yellow LED
    digitalWrite(yellowLED, HIGH);
    delay(3000); // Wait for 3 seconds
    digitalWrite(yellowLED, LOW); // Turn off Yellow LED
}
```
## Explanation of Code

- The code defines pins for each of the four LEDs and sets them as outputs in the `setup()` function.
- In the `loop()` function, it sequentially turns on each LED for 3 seconds before turning it off and moving to the next one.

### How to Use

1. Upload this code to your Arduino using the Arduino IDE.
2. Once uploaded, you should see each LED turn on one after another with a 3-second delay between them.

This setup provides a simple way to blink multiple LEDs in sequence using an Arduino. Adjustments can be made if you want different timings or additional functionality.

VIVA

Here are five potential questions and answers that could be asked during a viva covering the concepts from the Arduino LED blinking code:

- **Q1: What is the purpose of the `pinMode()` function in the setup?**
A1: The `pinMode()` function is used to configure the specified pins as outputs. This allows the Arduino to control the LEDs by sending electrical signals to these pins.
- **Q2: How does the code achieve a 3-second delay between LED transitions?**
A2: The code uses the `delay(3000)` function to create a 3-second pause between turning one LED off and the next one on. The argument 3000 represents 3000 milliseconds, which is equivalent to 3 seconds.
- **Q3: Explain the significance of using `digitalWrite()` function with HIGH and LOW parameters.**
A3: The `digitalWrite()` function is used to turn the LEDs on and off. When used with the HIGH parameter, it sends a voltage to the pin, turning the LED on. When used with LOW, it stops sending voltage, turning the LED off.
- **Q4: How are the LEDs connected to the Arduino board in this circuit?**
A4: The LEDs are connected to digital pins 2, 3, 4, and 5 of the Arduino. The anode (longer lead) of each LED is connected to its respective pin through a resistor, while the cathode (shorter lead) is connected to the ground.
- **Q5: Why are resistors used in the circuit, and what is their value?**
A5: Resistors are used to limit the current flowing through the LEDs to prevent them from burning out. In this circuit, 220-ohm resistors are used for each LED.