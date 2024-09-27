
## INSTALLING THE ENCLOSURE

This board does not have a "full closed" enclosure, because it needs a lot of air flow while stressing it with a lot of output current. So actually the "enclosure" will consists in two pieces: a simple flat base to screw to YULC with 3 M2 screws and the fan holder.

## STEP 1

First attach the inductor heatsink (the biggest one) as far to the right as possible, almost touching the fuse holder. Doing this way there is enough space for the regulator heatsink.

> [!IMPORTANT]  
Pay attention to place the heatsink in a way that it does not touch any other components, in particular the regulator IC one

In the end you can place the two heatsinks for the mosfet and then mount YULC on the base locking it in place with the help of the three smallest M2 screws
<center>
<p>
<img src="https://github.com/ale1800/YULC/blob/main/images/installation/base.jpg" width="600">
</p>
</center>

## STEP 2

Use other 4 M2 screws to mount the facing down fan on top of the holder and then connect it to YULC thorugh the dedicated JST connector. 
<center>
<p>
<img src="https://github.com/ale1800/YULC/blob/main/images/installation/fan.jpg" height="300">
<img src="https://github.com/ale1800/YULC/blob/main/images/installation/fan_to_pcb.jpg" width="500">
</p>
</center>

## STEP 3

Now, with the help of the two longer screws, connect the fan holder to the two pillars of the base

<center>
<p>
<img src="https://github.com/ale1800/YULC/blob/main/images/installation/complete.jpg" width="600">
</p>
</center>

Your YULC is completely assembled, you can proceed with the [software configuration](https://github.com/ale1800/YULC/tree/main?tab=readme-ov-file#software-configuration)

## BONUS

### DIN BRACKET
The base has two more holes for M2 screws that can be used to design other types of support, like a din-mounting bracket, taken from [thingiverse](https://www.thingiverse.com/thing:2613804) and modified a bit.

<p>
<img src="https://github.com/ale1800/YULC/blob/main/images/v2.1/din-combined.jpg" width="600"> 
</p>

If you want to install something like this, you have to do that before [STEP 1](#step-1)

### INMP441 MIC ADAPTER

If you would like to use the INMP441 microphone breakout board in combination with the Sound Reactive usermod, you can find [here](https://github.com/ale1800/YULC/blob/main/Schematic/mic.zip) the gerber file of the tailor-made adapter.



<center>
<p>
<img src="https://github.com/ale1800/YULC/blob/main/images/mic/PXL_20240927_054954133.jpg" height="300">
<img src="https://github.com/ale1800/YULC/blob/main/images/mic/PXL_20240927_055002209.jpg" height="300">
</p>
</center>

It uses the following pins:
| YULC Pin | INMP441 Pin |
| --- | ---|
| 3V | 3V |
|  GPIO 43 (TX) | SD |
|  GPIO 44 (RX) | WS |
|  GND | GND, L/R |
| GPIO 38 | SCK |
