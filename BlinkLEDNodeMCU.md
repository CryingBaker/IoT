To blink four LEDs one by one with a 3-second delay using a NodeMCU (ESP8266), you can follow the steps below, which include the circuit setup and the corresponding Arduino code.

## Components Required

- **NodeMCU (ESP8266)**
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
3. **Wiring to NodeMCU**:
    - Connect the anode of the Red LED to pin D1 on the NodeMCU.
    - Connect the anode of the Green LED to pin D2 on the NodeMCU.
    - Connect the anode of the Blue LED to pin D3 on the NodeMCU.
    - Connect the anode of the Yellow LED to pin D4 on the NodeMCU.
    - Connect all cathodes to ground.

## Arduino Code

Here is a simple code that will blink four LEDs one by one with a 3-second delay:

```cpp
// Define pin numbers for LEDs
const int redLED = D1;    // Red LED connected to pin D1
const int greenLED = D2;  // Green LED connected to pin D2
const int blueLED = D3;   // Blue LED connected to pin D3
const int yellowLED = D4; // Yellow LED connected to pin D4

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

1. Upload this code to your NodeMCU using the Arduino IDE.
2. Once uploaded, you should see each LED turn on one after another with a 3-second delay between them.

This setup provides a simple way to blink multiple LEDs in sequence using a NodeMCU. Adjustments can be made if you want different timings or additional functionality.

OR ELSE     — According to Problem Statement 

To control an LED connected to the ESP8266 NodeMCU by creating a web server in station mode, you can follow the steps outlined below. This process involves setting up the NodeMCU to connect to a Wi-Fi network, creating a web server, and providing a simple interface to turn the LED on and off.

## Components Required

- **ESP8266 NodeMCU**
- **1 LED** (any color)
- **1 Resistor** (220 ohms)
- **Breadboard**
- **Jumper wires**

## Circuit Setup

1. **Insert the LED** into the breadboard:
    - Place the LED in the breadboard.
    - Connect the longer lead (anode) of the LED to a separate row on the breadboard.
2. **Connect Resistor**:
    - Connect a 220-ohm resistor from the shorter lead (cathode) of the LED to ground.
3. **Wiring to NodeMCU**:
    - Connect the anode of the LED to GPIO pin D2 (or any available GPIO pin) on the NodeMCU.
    - Connect all cathodes to ground.

## Arduino Code

Here is a sample code that sets up a web server on the NodeMCU to control an LED:

```cpp
#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>

// Replace with your network credentials
const char* ssid = "YOUR_SSID"; // Your Wi-Fi SSID
const char* password = "YOUR_PASSWORD"; // Your Wi-Fi Password

// Create an instance of the server
ESP8266WebServer server(80);

// Define pin for LED
const int ledPin = D2;

void setup() {
    Serial.begin(115200);
    pinMode(ledPin, OUTPUT); // Set LED pin as output

    // Connect to Wi-Fi
    WiFi.begin(ssid, password);
    while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
    }
    Serial.println("Connected to Wi-Fi");
    Serial.print("IP address: ");
    Serial.println(WiFi.localIP());

    // Define routes for web server
    server.on("/", handleRoot); // Handle root URL
    server.on("/led/on", handleLEDOn); // Handle LED ON request
    server.on("/led/off", handleLEDOff); // Handle LED OFF request

    // Start server
    server.begin();
}

void loop() {
    server.handleClient(); // Handle incoming client requests
}

// Function to handle root URL
void handleRoot() {
    String html = "<html><body><h1>Control LED</h1>";
    html += "<p><a href=\\"/led/on\\"><button>Turn ON</button></a></p>";
    html += "<p><a href=\\"/led/off\\"><button>Turn OFF</button></a></p>";
    html += "</body></html>";
    server.send(200, "text/html", html); // Send HTML response
}

// Function to handle turning ON the LED
void handleLEDOn() {
    digitalWrite(ledPin, HIGH); // Turn ON LED
    server.send(200, "text/html", "LED is ON! <a href=\\"/\\">Go Back</a>");
}

// Function to handle turning OFF the LED
void handleLEDOff() {
    digitalWrite(ledPin, LOW); // Turn OFF LED
    server.send(200, "text/html", "LED is OFF! <a href=\\"/\\">Go Back</a>");
}

```

### Explanation of Code

- The code connects to your specified Wi-Fi network and sets up a web server on port 80.
- It defines three routes:
    - The root URL (`/`) displays buttons for turning the LED on and off.
    - The `/led/on` route turns on the LED.
    - The `/led/off` route turns off the LED.
- When you access these URLs from a web browser, it will control the state of the LED accordingly.

### How to Use

1. Replace `YOUR_SSID` and `YOUR_PASSWORD` in the code with your actual Wi-Fi credentials.
2. Upload this code to your NodeMCU using the Arduino IDE.
3. Open the Serial Monitor (set baud rate to 115200) after uploading. Note down the IP address assigned to your NodeMCU.
4. Open a web browser and enter the IP address in the address bar.
5. You will see buttons to turn the LED on and off.

This setup allows you to control an LED connected to your ESP8266 NodeMCU through a simple web interface, demonstrating how to create a basic web server in station mode.

VIVA

Here are the top 5 potential questions and answers that could be asked in a viva covering the concepts from the code:

- **Q1: What is the purpose of using the ESP8266WiFi and ESP8266WebServer libraries in this code?**
A1: The ESP8266WiFi library is used to connect the NodeMCU to a Wi-Fi network, while the ESP8266WebServer library is used to create a web server on the NodeMCU. These libraries enable the device to connect to the internet and serve web pages, allowing for remote control of the LED.
- **Q2: How does the code handle different routes for controlling the LED?**
A2: The code defines three main routes:
    1. Root URL ("/") displays buttons for turning the LED on and off.
    2. "/led/on" route turns on the LED.
    3. "/led/off" route turns off the LED.
    These routes are handled by separate functions (handleRoot, handleLEDOn, handleLEDOff) which are called when the corresponding URL is accessed.
- **Q3: Explain the setup() function in the code.**
A3: The setup() function initializes the serial communication, sets the LED pin as output, connects to the Wi-Fi network, prints the assigned IP address, defines the routes for the web server, and starts the server. This function runs once when the NodeMCU boots up and prepares the device for its main operations.
- **Q4: How does the code create a simple web interface for controlling the LED?**
A4: The code generates an HTML page in the handleRoot() function, which includes two buttons: one for turning the LED on and another for turning it off. When these buttons are clicked, they send requests to the "/led/on" or "/led/off" routes, which then control the LED state. The web interface is served when a user accesses the NodeMCU's IP address in a web browser.
- **Q5: What is the purpose of the loop() function in this code, and why is it important?**
A5: The loop() function continuously calls server.handleClient(), which allows the NodeMCU to listen for and handle incoming HTTP requests from clients. This is crucial for the web server functionality, as it ensures that the device can respond to user interactions through the web interface at any time.