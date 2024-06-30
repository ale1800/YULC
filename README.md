# YULC (Yes, a USB-C Led Controller)

![yulc](https://github.com/ale1800/YULC/assets/53172176/b7f9087c-cb34-41fb-9961-a1b0314f90dd)
#### Dual Power Inputs
**YULC** provides two ways to fuel your LED creations. Choose from the USB-C port supporting PD protocol (**5V, 9V, 12V, 15V, and 20V**) for up to **100W (5A@20V**), or use a separate power supply via the barrel jack (**up to 20A@24V**).

#### Versatile Power Distribution
**YULC** empowers you to choose how your strips receive power:
**Direct Power**: Route the input power straight to the strips for maximum efficiency.
**Bucked-Down Power**: Utilize the built-in converter **to deliver safe 5V or 12V to your strips,** with a maximum of 20A. Simply populate one of the two fuse holders to select your preference.

For example, you have 4 ways to power your 5V WS2812b strip.

1. **Classic power supply at 5V** with a barrel jack, populating the fuse for the direct output. (bypassing the buck converter)
2. **Selecting 5V from the PD** and routing to the strip populating the direct output fuse (bypassing the buck converter)
3. Populating the fuse of the regulated output, you can choose a **barrel jack power supply that can provide more than 5V (with the desired power)** and regulate at 5V using the buck converter
4. **Regulating at 5V using the PD protocol of the USB-C,** so selecting a voltage of 9V or higher 





### Dual Channel Control for Seamless Lighting:

#### Independent Control
**YULC** boasts two separate LED channels, each equipped with a level shifter to ensure clean data transmission even for extended LED strips.
#### Simplified Strip Control
Dedicated power MOSFETs eliminate the need for external relays, to physically turn on and off the strips saving a considerable amount of power for long ones. This allows for direct control and also smooth dimming via PWM for simpler strips.


### Built-in Safety Measures for Peace of Mind:

#### Multi-Layered Protection:

- **The main fuse** safeguards against overcurrents.

- **ESD protection** shields the PD and ESP32-S3 USB data from electrostatic discharge.
- **Overvoltage transient protection** on the USB power line prevents damage from voltage spikes.
- **Back-to-back MOSFET configuration** ensures safe programming while using an external power supply.
- **YULC negotiates voltage with your USB charger.** If an incompatible voltage is detected, the current is automatically blocked to protect your LED strips and nothing will be powered.
- **The ESP32-S3 microprocessor can detect the blown fuse**, making troubleshooting easier in case of a shorting output or an overcurrent event.
