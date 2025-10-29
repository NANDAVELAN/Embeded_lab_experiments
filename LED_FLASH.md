## Name: Nandavelan SPS
## Reg No: 212223060182
## Slot : 4X4-5

# FLASHING-OF-LEDS-WITH-LPC-1768

# AIM: 
   To interface and toggle the led with ARM LPC 1768 microprocessor           
           
# COMPONENTS REQUIRED:

##  HARDWARE:
ARM LPC1768
LED

## SOFTWARE:
KEIL MICRO VISION 4.0 IDE

# PROCEDURE:

## Steps to Create and Build a Project in Keil for LPC1768

1. **Open Keil Software**
   - Go to **Project → New uVision Project**.

2. **Create a New Project**
   - Browse to your project folder.
   - Provide a project name and click **Save**.

3. **Select the Device**
   - In the *Select Device for Target* window, choose **NXP → LPC1768** (founded by Philips).
   - Click **OK**.

4. **Include Startup Code**
   - When prompted, click **Yes** to include the *LPC17xx Startup file*.

5. **Create a New File**
   - Go to **File → New** to create a new source file.
   - Type your program code.

6. **Save the File**
   - Save the file as **main.c** (e.g., `abc.c`).

7. **Add Files to Project**
   - Right-click **Target 1 → Add Existing Files to Group 'Source Group 1'**.
   - Add both **main.c** and **system_LPC17xx.c** files.

8. **Build the Project**
   - Click **Build**.
   - Fix any compiler **errors or warnings** if present.

9. **Generate the .bin File**
   - If code compiles with no errors but no `.bin` file is generated:
     - Right-click on **Target Options**.
     - Select options for **generating .bin file**.

10. **Set Memory Start Address**
    - Set **IROM1 Start Address** to `0x2000`.
    - *(Bootloader will occupy 0x0000 – 0x2000, so the application starts from 0x2000.)*

11. **Command to Generate .bin File from .axf**
    ```bash
    fromelf --bin projectname.axf --output filename.bin
    ```

12. **Set Include Paths**
    - In **C/C++ → Include Paths**, add:  
      `desktop (00-libfiles)`

13. **Rebuild the Project**
    - Rebuild the project.
    - The `.bin` file is now generated.

14. **Verify the Output**
    - Check your project folder for the generated **.bin** file.


## ADD FILES:
Target1:

Source group1:
Startuplpc17xx.s, main.c (t), delay.c (t), systemlpc17xx.c (t), gpio.c (t)

Header:
Delay.h, stdutils.h, gpioi.h

# PIN DIAGRAM :

<img width="984" height="627" alt="image" src="https://github.com/user-attachments/assets/90b88341-046e-4764-a93e-3e5fc09c0ce4" />


# CIRCUIT DIAGRAM:

<img width="768" height="431" alt="image" src="https://github.com/user-attachments/assets/23f546de-ed2a-4200-b0ae-70c66de58cd4" />

 
# PROGRAM:

```
#include <lpc17xx.h>
#include "delay.h" //User defined library which conatins the delay routines #include "gpio.h"
#define LED P1_29 // Led is connected to P1.29
/* start the main program */ int main()
{
SystemInit(); //Clock and PLL configuration
GPIO_PinFunction(LED,PINSEL_FUNC_0); // Configure Pin for Gpio
GPIO_PinDirection(LED,OUTPUT); // Configure the pin as OUTPUT GPIO_PinWrite(LED,LOW);
while(1)
{
/* Turn On all the leds and wait for 100ms */

GPIO_PinWrite(LED,HIGH); // Make all the Port pin as high
DELAY_ms(100);
GPIO_PinWrite(LED,LOW); // Make all the Port pin as low DELAY_ms(100);
}
}
```
 
# Output:
![20250826_162012](https://github.com/user-attachments/assets/89b71b64-b91d-4003-8cfe-c0e54e651db2)

# Result:
The experiment on toggling an LED with the ARM LPC1768 microcontroller was successfully performed. The LED flashed ON and OFF at regular intervals as programmed, confirming correct interfacing and functioning of the GPIO operations. The code compiled without errors, and all hardware connections were verified to work as expected. The experiment demonstrated the basic use of GPIO for output and timing control using software delays.


