#  GAS-LEAK-DETECTION-SYSTEM-USING-GAS-SENSOR

## Aim:
	
To measure the air quality using Gas Sensor  MQ-2 with Arduino UNO Board/ESP-32 using Tinker CAD.

## Hardware / Software Tools required:
	
PC/ Laptop with Internet connection
Tinker CAD tool (Online)
Arduino UNO Board/ESP-32
Gas sensor (MQ-2)
	
## Circuit Diagram:

![image](https://github.com/user-attachments/assets/d6e3e73b-45e7-4a69-b467-c6525de37b49)

## Theory :

The Arduino Uno is powered by the ATmega328P, an 8-bit microcontroller that runs at 16 MHz. It has 32 KB of flash memory, 2 KB of SRAM, and 1 KB of EEPROM. The board has 14 digital I/O pins (of which 6 can be used as PWM outputs) and 6 analog input pins. These pins allow the board to interface with various sensors, actuators, and other devices.

The Arduino Uno can be powered via a USB connection or an external power supply. The board has a built-in voltage regulator to manage power from 7 to 12 volts.

The board is programmable using the Arduino IDE (Integrated Development Environment), which supports a simplified version of C/C++. The code, known as a "sketch," is uploaded to the board via a USB connection. The Uno has a USB-B port, which is used for communication with a computer. The USB connection also powers the board when connected. The board includes a reset button that restarts the microcontroller, useful during programming and troubleshooting. The In-Circuit Serial Programming (ICSP) header allows for low-level programming of the microcontroller or firmware updates. The Uno has a built-in LED on pin 13, commonly used for simple tests and debugging.

## Procedure:

**Step 1: Set Up the Tinkercad Environment**

1. Log in to Tinkercad: Open Tinkercad in your web browser and log in to your account.
2. Create a New Circuit: In the Tinkercad dashboard, click on "Circuits" and then select "Create New Circuit."

**Step 2: Add Components to the Circuit**

1. Arduino Uno: Drag an Arduino Uno board from the components panel onto the workspace.
2. Gas Sensor: Search for the TMP36 sensor in the components panel and drag it into the workspace.
3. Breadboard: Drag a small breadboard to the workspace to help with wiring connections.
4. Resistor (Optional): A resistor may not be necessary for this simple setup, but you can include it for more accurate readings.
5. Wires: Use wires to connect the components.

**Step 3: Connect the MQ-2 Gas Sensor to Arduino:**

- MQ-2 Pins:
  - VCC: Connect this pin to the Arduino 5V pin.
  - GND: Connect this pin to the Arduino GND pin.
  - Analog Output (A0): Connect this pin to an analog input pin on the Arduino (e.g., A0).
  - Digital Output (D0): (Optional) Connect this pin to a digital input pin on the Arduino if you want to use the sensor's digital threshold output.

**Breadboard Wiring:**

- MQ-2 VCC to Arduino 5V: Use a wire to connect the VCC pin of the MQ-2 sensor to the 5V rail on the breadboard (which is connected to Arduino 5V).
- MQ-2 GND to Arduino GND: Connect the GND pin of the MQ-2 sensor to the ground rail on the breadboard (connected to Arduino GND).
- MQ-2 Analog Output (A0) to Arduino Analog Pin (A0): Connect the analog output pin of the sensor to Arduino's A0 pin.
- (Optional) MQ-2 Digital Output (D0) to Arduino Digital Pin (e.g., D2): Connect the digital output pin if you want to detect gas concentration threshold digitally.

**Step 4: Write the Arduino Code**

- Code Editor: Click on the "Code" button at the top of the Tinkercad workspace to open the code editor.
- Set the Coding Mode: Ensure the editor is in "Text" mode to write your code in C/C++.
- Enter the Code: Write the following code from the MQ-2  sensor

**Step 5: Simulate the Circuit**

- Start Simulation: Click the "Start Simulation" button at the top of the workspace to run the circuit and code.
- Monitor Output: Open the serial monitor by clicking the "Serial Monitor" button to view the temperature readings in both Celsius and Fahrenheit.

**Step 6: Troubleshoot and Refine**

- Check Connections: Ensure that all connections are made correctly on the breadboard and the Arduino.
- Adjust Code: If needed, tweak the code to improve accuracy or change the format of the output.

**Step 7: Save Your Work**

- Stop Simulation: Click "Stop Simulation" to end the simulation.
- Save the Circuit: Click "Save" to keep your circuit design and code for future use.

## Program:

```cpp
#include <LiquidCrystal.h>
// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  Serial.begin(9600);
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  pinMode(13,OUTPUT);
  pinMode(7,OUTPUT);
  pinMode(6,OUTPUT);
}

void loop() {
  int gas_data;
  gas_data = analogRead(A0);
  lcd.setCursor(00,00);
  lcd.print("Gas :");
  lcd.setCursor(6,00);
  lcd.print(gas_data);
  if(gas_data > 500){
    digitalWrite(13,HIGH);
    delay(100);
    digitalWrite(13,LOW);
    lcd.setCursor(00,1);
    lcd.print("DANGER");
  }else if(gas_data > 400){
    digitalWrite(6,HIGH);
    delay(100);
    digitalWrite(6,LOW);
    lcd.setCursor(00,1);
    lcd.print("WARNING");
  }else {
    digitalWrite(7,HIGH);
    lcd.setCursor(00,1);
    lcd.print("SAFE");
  }
  Serial.println(gas_data);
  delay(100);
  lcd.clear();
}
```

## Output:

![image](https://github.com/user-attachments/assets/78ff5df8-7b10-466a-9600-3645f6d9b599)

## Result:

The gas leak detection system was successfully implemented using Arduino UNO and MQ-2 gas sensor in Tinkercad. The system effectively monitored gas concentration levels in real-time, displaying analog readings on a 16x2 LCD screen along with corresponding safety status indicators. When gas levels were below 400, the green LED illuminated with "SAFE" status; levels between 400-500 triggered the yellow LED with "WARNING" message; and levels above 500 activated the red LED with "DANGER" alert. The serial monitor provided continuous numerical data logging for analysis. The circuit demonstrated proper threshold-based decision making and visual feedback through LEDs and LCD, proving its effectiveness as a safety monitoring system for detecting hazardous gas leaks in real-world applications.
