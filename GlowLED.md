To glow two LEDs serially using a NodeMCU (ESP8266), you can follow the steps outlined below, which include the circuit setup and the corresponding Arduino code.

## Components Required

- **NodeMCU (ESP8266)**
- **2 LEDs** (e.g., Red and Green)
- **2 Resistors** (220 ohms for each LED)
- **Breadboard**
- **Jumper wires**

## Circuit Setup

1. **Insert the LEDs** into the breadboard:
    - Place the Red LED and Green LED in a row.
    - Connect the longer lead (anode) of each LED to a separate row on the breadboard.
2. **Connect Resistors**:
    - Connect a 220-ohm resistor from the shorter lead (cathode) of each LED to the ground rail on the breadboard.
3. **Wiring to NodeMCU**:
    - Connect the anode of the Red LED to pin D1 on the NodeMCU.
    - Connect the anode of the Green LED to pin D2 on the NodeMCU.
    - Connect all cathodes to ground.
- Connect all cathodes to ground.

## Arduino Code

Here is a simple code that allows you to control two LEDs using serial commands:

```cpp
#define RED_LED D1    // Define pin for Red LED
#define GREEN_LED D2  // Define pin for Green LED

void setup() {
    Serial.begin(115200); // Start serial communication at 115200 baud rate
    pinMode(RED_LED, OUTPUT);    // Set RED_LED pin as output
    pinMode(GREEN_LED, OUTPUT);  // Set GREEN_LED pin as output
}

void loop() {
    if (Serial.available()) { // Check if data is available to read
        String command = Serial.readStringUntil('\\n'); // Read command until newline

        if (command.equalsIgnoreCase("RedOn")) { // If command is "RedOn"
            digitalWrite(RED_LED, HIGH);  // Turn on Red LED
            digitalWrite(GREEN_LED, LOW); // Turn off Green LED
            Serial.println("Red LED is ON");
        } else if (command.equalsIgnoreCase("GreenOn")) { // If command is "GreenOn"
            digitalWrite(GREEN_LED, HIGH); // Turn on Green LED
            digitalWrite(RED_LED, LOW);     // Turn off Red LED
            Serial.println("Green LED is ON");
        } else if (command.equalsIgnoreCase("Off")) { // If command is "Off"
            digitalWrite(RED_LED, LOW);     // Turn off Red LED
            digitalWrite(GREEN_LED, LOW);   // Turn off Green LED
            Serial.println("Both LEDs are OFF");
        }
    }
}

## Explanation of Code

- The code initializes serial communication and sets up pins for both LEDs as outputs.
- In `loop()`, it checks if there are any incoming serial commands.
- Depending on the command received:
    - `RedOn`: Turns on the Red LED and turns off the Green LED.
    - `GreenOn`: Turns on the Green LED and turns off the Red LED.
    - `Off`: Turns off both LEDs.

### How to Use

1. Upload this code to your NodeMCU using the Arduino IDE.
2. Open the Serial Monitor (Ctrl + Shift + M) in the IDE.
3. Set it to 115200 baud rate.
4. You can type commands such as `RedOn`, `GreenOn`, or `Off` in the Serial Monitor to control the LEDs.

This setup allows you to control two LEDs serially using a NodeMCU with simple commands sent through the Serial Monitor.
IVA

Here are the top 5 potential questions and answers that could be asked in a viva covering the concepts from the code:

- **Q1: What is the purpose of the code and how does it control the LEDs?**
A1: The code allows for serial control of two LEDs connected to a NodeMCU (ESP8266). It uses serial commands to turn on the red LED, turn on the green LED, or turn off both LEDs. The control is achieved through digital output pins and serial communication.
- **Q2: How is the serial communication set up in the code?**
A2: The serial communication is initialized in the `setup()` function with a baud rate of 115200. In the `loop()` function, the code checks for available serial data and reads commands until a newline character is encountered.
- **Q3: What are the valid commands for controlling the LEDs and how are they processed?**
A3: The valid commands are "RedOn", "GreenOn", and "Off". The code uses `if-else` statements to check the received command (case-insensitive) and performs the corresponding action:
    - "RedOn": Turns on the red LED and turns off the green LED
    - "GreenOn": Turns on the green LED and turns off the red LED
    - "Off": Turns off both LEDs
    The code also sends a confirmation message through serial communication for each action.
- **Q4: How are the LED pins configured in the code?**
A4: The LED pins are defined using `#define` statements at the beginning of the code. RED_LED is connected to pin D1, and GREEN_LED is connected to pin D2. In the `setup()` function, these pins are configured as outputs using `pinMode()`.
- **Q5: What is the circuit setup for this experiment?**
A5: The circuit setup involves:
    - Two LEDs (red and green) inserted into a breadboard
    - 220-ohm resistors connected to the cathode of each LED
    - The anode of the red LED connected to pin D1 on the NodeMCU
    - The anode of the green LED connected to pin D2 on the NodeMCU
    - All cathodes connected to ground
    This setup allows for individual control of each LED through the NodeMCU.