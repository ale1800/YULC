# YULC (Yes, a USB-C Led Controller)

## If you want to stay tuned, this is YULC on [Crowd Supply](https://www.crowdsupply.com/aaelectronics/yulc)

![yulc](https://github.com/ale1800/YULC/assets/53172176/b7f9087c-cb34-41fb-9961-a1b0314f90dd)
**YULC** is your perfect mate for powering your lightings at 5, 12 or 24V. Thanks to its compact form factor (a 3D printable case is coming), it can be placed almost everywhere, it features a lot of protections to **ensure safety for both the charger and the strips**, and in the meanwhile, **can provide a lot of juice to feed very power-hungry lights setup.** 
It also boasts an handy **built-in buck regulator** that from a maximum of 24V ensures safe 5V or 12V to your output. This mean that is also possible to use 18,19,...,24V external power supply (USB-C or barrel jack) taking advantage of their higher total power output and converting them to 5V or 12V increasing the output current.
Furthermore, on the back of the board there is a **powerful ESP32-S3, directly programmable from the USB-C**, that allows you to manage even more complex effects and to run heavy tasks.  
So, in few words, **YULC** consists in a full-featured board that can replace a lot of wiring messes, optimizing space and debug time in a reliable way.

**Deeping in the details**:

### Dual Power Inputs
**YULC** provides two ways to feed your LED creations. Choose from the USB-C port supporting **PD 3.0 protocol (5V, 9V, 12V, 15V, and 20V) for up to 100W (5A@20V)**, or use a separate power supply via the barrel jack **(up to 20A@24V)**.
The ESP32-S3 and all the other components are powered by a secondary buck converter.

### Versatile Power Distribution
**YULC** empowers you to choose how your strips receive power:  

* **Direct Power**: Route the input power straight to the strips for maximum efficiency.  
* **Bucked-Down Power**: Utilize the built-in converter to deliver 5V or 12V to your strips, with a maximum of 20A. Simply populate one of the two fuse holders to select your preference.

For example, you have **4 ways** to power your 5V WS2812B strip:

* Classic power supply at 5V with a barrel jack, populating the fuse for the direct output. (bypassing the buck converter)
* Selecting 5V from the PD and routing to the strip populating the direct output fuse (bypassing the buck converter)
* Populating the fuse of the regulated output, you can choose a barrel jack power supply that can provide more than 5V (with the desired power) and regulate at 5V using the buck converter
* Regulating at 5V using the PD protocol of the USB-C, so selecting a voltage of 9V or higher

Here you can have a look to how the power path works:






[![Concept map (6)](https://github.com/ale1800/ESP32-board/assets/53172176/7c49a46b-c15e-45c9-bb84-2c160c00b566)](https://github.com/ale1800/YULC/blob/main/images/Concept%20map.png)

Powering all the logic and the ESP32-S3 with a dedicated secondary power stage without relying on the main one ensures that in case of a blowing fuse, everyhitng will still work as expected. So replacing the fuse on-the-fly will be the only thing you'll need to be again ready to go.


### Dual Channel Control for Seamless Lighting:

**YULC** comes with two separate LED channels, each equipped with a level shifter to ensure clean data transmission even for extended LED strips. You won't need any external level shifter, neither sacrifying a pixel to boost the data voltage.

**Complete Strip Control**  

**Dedicated power MOSFETs (one for channel) eliminate the need for external relays**, to physically turn on and off the strips saving a considerable amount of power for long ones. 
These allow for a direct control and also smooth dimming via PWM for simpler strips.

![PXL_20240702_170940775](https://github.com/ale1800/ESP32-board/assets/53172176/34b24297-1c93-43cd-b487-1ca270770319) 

https://github.com/ale1800/ESP32-board/assets/53172176/a9922877-4f54-4cd5-a90a-000a9c27c625








### Built-in protections   

* **The main blade fuse directly protects the regulator (and so the charger) against overload faults**. You can choose to use a 20A to make the regulator not to reach its physical current limit or you can resize it to 5/10/15A according to what your strips need.
  The holders are compatible with both the **mini** and **standard** dimension blade fuses.

* **ESD protection shields the PD and ESP32-S3 USB data from electrostatic discharge.**

* **Overvoltage transient protection on the USB power line prevents damage from voltage spikes.**

* **Back-to-back MOSFET configuration ensures safe programming while using an external power supply.** With the switch on **"EXT"**, you'll be able to power **YULC** with an external power supply up to 24V while programming it using your laptop's USB-C port.

* **YULC safely negotiates voltage with your USB-C charger.** If the charger can not provide the requested voltage, **the current is automatically blocked and nothing will be powered**. Also during the negotiation, nothing will be powered until the voltage 
  has been successfully provided by the charger. This safety mechanism grants that a wrong voltage won't damage components or the connected LED strips with too high/low voltage compared to the selected one.

* **The ESP32-S3 microcontroller can detect the blown fuse**, making troubleshooting easier in case of a shorting output or an overcurrent event.   

### Designed for Development and Creativity:

* **Hardware Button**: This board features a physical button for easy control of your strips, allowing you to turn them on/off or switch lighting effects. It's also the BOOT button of the ESP32-S3.
* **Breadboard-Friendly Header**: It exposes a multitude of ESP32-S3 pins via a breadboard-compatible header. This simplifies the process of adding functionalities like microphones, potentiometers, and more to your lighting project.
* **GPIO Header:**
  
  |   Pin    |  Function |
  |----------|-----------|
  |  GPIO 12 |     IO    |
  |  GPIO 17 |     IO    |
  |  GPIO 18 |     IO    |
  |  GPIO 39 |     IO    |
  |  GPIO 40 |     IO    |
  |  GPIO 41 |     IO    |
  |  GPIO 42 |     IO    |
  |  5V      |   Power   |
  |  3V      |   Power   |
  |  GND     |  Ground   |
  |  GPIO 44   |    TX     |
  |  GPIO 43   |    RX     |
* **Used GPIO:**

  | Pin | Function |
  | --- | ---|
  | GPIO 0 (DO) | Boot/User Button |
  |  GPIO 1 (DO) | Led Data 1 |
  |  GPIO 2 (DO) | Led Data 2 |
  |  GPIO 21 (DO) | Mosfet 1 |
  | GPIO 47 (DO) | Mosfet 2 |
  | GPIO 7 (AI) | Fuse sense |

