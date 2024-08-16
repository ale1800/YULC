![Static Badge](https://img.shields.io/badge/Crowd_Supply-brightgreen?link=https%3A%2F%2Fwww.crowdsupply.com%2Faaelectronics%2Fyulc)
![Static Badge](https://img.shields.io/badge/AAElectronics-lightblue?label=Discord&link=https%3A%2F%2Fdiscord.com%2Finvite%2FByGBf97C)


# YULC (Yes, a USB-C Led Controller)

![yulc](https://github.com/ale1800/YULC/blob/main/images/yulc.jpg)
**YULC** is your perfect mate for powering your lightings at 5, 12 or 24V. Thanks to its compact form factor (a 3D printable case is coming), it can be placed almost everywhere, it features a lot of protections to **ensure safety for both the charger and the strips**, and in the meanwhile, **can provide a lot of juice to feed very power-hungry lights setup.** 
It also boasts an handy **built-in buck regulator** that from a maximum of 24V ensures safe 5V or 12V to your output. This mean that is also possible to use 18,19,...,24V external power supply (USB-C or barrel jack) taking advantage of their higher total power output and converting them to 5V or 12V increasing the output current.
Furthermore, on the back of the board there is a **powerful ESP32-S3, directly programmable from the USB-C**, that allows you to manage even more complex effects and to run heavy tasks.  
So, in few words, **YULC** consists in a full-featured board that can replace a lot of wiring messes, optimizing space and debug time in a reliable way.

## HOW IT WORKS


Here you can have a look to how the power path works:

![Concept map (6)](https://github.com/ale1800/YULC/blob/main/images/Concept%20map.png)

Powering all the logic and the ESP32-S3 with a dedicated secondary power stage without relying on the main one ensures that in case of a blowing fuse, everyhitng will still work as expected. So replacing the fuse on-the-fly will be the only thing you'll need to be again ready to go.

### YULC'S FEATURES

![Board](https://github.com/ale1800/YULC/blob/main/images/list.png)

1) This is the main jumper that you have to select before anything else and before powering the board. If you join the **"EXT"** pins, YULC will be powered through the barrel jack power supply, not through the USB-C. So you can use a power supply up to 24V and then decide if you want to buck it to 5V or 12V or use it directly to the output bypassing the buck converter. With this selection, you are also able to safely program YULC through the USB-C while powering everything from the external power supply thanks to a back-to-back mosfet configuration. To do that **you have to select 5V from the PD selection voltage (2)**. There will also be those 5V on the board but they won't power anything (To prove that just disconnect the barrel jack power supply and the board will be turned off).
Instead, if you select **"USB"** pins, everything will be powered from the USB-C according to the voltage selected. As before, you can choose to buck the voltage to 12 or 5V or use it directly. **In this case do not connect also the barrel jack!**
   
2) USB-C PD Voltage selection. **Note that these voltages are the one you are asking to the charger, not the ones you surely have on the board.** Selecting 20V, if the charger can provide them, the negotiation will end successfully, mosfets will let current flow and everything will be powered on. But if the charger is not able to do that, the negotiation will fail and the board will stay off. To help you debug that, the leds "OK" or "BAD" will lights up according to the negotiation result. Pay attention to what chargers you want to use. It should have a label with the list of voltages it can provide, so be sure to ask for that supported voltages, otherwise the negotiation will fail. Also consider the amount of power you need for your led strips and the power the charger can spit out. If you have 5V strips like WS2812b and you want 6A at the output (so 30W), **be sure to ask the for a voltage/current combo the charger can offer that can give those 30W and the buck it to 5V through the converter to have than current you want at the output.**

3) This is the buck converter output regulation. Populate horizontally the pins according to voltage you want to have at the output. If your input is lower or same as the output, just do not use the buck converter and route it directly. These voltages can slightly decrease as the output current increase. The sum of the resistance of the buck converter + DC resitance of the inductor + resistance of the fuse + resistance of terminal is around 20/25mV, so expect a drop voltage of **V = 0.025 * A** (Output current).
You can source up to 20A from the IC. **Please always use the given heatsinks (both for the IC and the inductor) and the 5V fan to be on the safe side.**
Keep it populated even if you don't want to use it. The buck IC will automatically enter in an energy save mode when the load is really small or even is not present.

4) These two fuse holders are not one for channel as it could seem. The two channels share the same fuse. But there are two fuses because you have to select only one at a time according to what output you need. If you need the buck converter you have to populate the "REGULAT. OUT" fuse. Otherwise, if you want the input voltage routed directly to the output, populate the "DIRECT OUT" one. **NEVER POPULATE BOTH AT THE SAME TIME, IT WILL SHORT THE CONVERTER IC**
These holders are compatible with both the standard automotive blade fuses and the mini blase fuses, but for higher currents the standard blade fuse is suggested thanks to a better contact with the holder's metal

5)YULC's has 10 output terminals, 5 for each channel

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

