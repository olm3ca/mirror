## Creating a Smart Mirror from a Lululemon Mirror
Now that the company has started to abandon the product, it's time to open it up and make it a more functional smart mirror.

Note: If you have a newer model Mirror (my unit is Rev08, ordered November 2022), the good news is you may have a BOE display which is the same display used in many TVs from Vizio, ONN and Samsung. This guide is primarily dedicated to that model as it is very easy to place a TV mainboard into the Mirror to display whatever you want.

To check, simply lay down your Mirror, unscrew the base (if used) and four screws on the back side. Lift up the metal case and look for BOE, as shown below where the red circle is:

<img src="Mirror.jpg" width="900">

If your Mirror is a BOE display, read below for an easy solution. If you have Samsung or any other display, the steps to work with your panel is still a work in progress. 

--------------------------------------------------------------------------------------------------------------------------------------------------------
### Before you begin, 
**By continuing, you acknowledge that you have read and understood the contents of the following disclaimer, and consent to their terms.**

The process described in this document could cause irreversible damage to your Mirror, and you should prepare yourself for that outcome before you begin. I accept absolutely no responsibility for the consequences of anyone choosing to follow or ignore any of the instructions in this document, and make no guarantees about the quality or effectiveness of the software in this repo.

--------------------------------------------------------------------------------------------------------------------------------------------------------

## Table of Contents

- [Project Goals](#project-goals)
- [Hardware Versions](#hardware-versions)
- [Method](#method)
- [Other Mirror Models](#other-mirrors)
- [Steps to Repin LVDS](#how-to-repin)
- [Accessories](#accessories)

--------------------------------------------------------------------------------------------------------------------------------------------------------

### Project Goals:
The goal is to allow the Mirror to accept other connections via HDMI. This could be a rasberry pi or other streaming device. For my Mirror, I want to use [Magic Mirror](https://magicmirror.builders/) using a small computer like a pi to fit inside the Mirror. I also want to keep the same psu, backlight inverter, control boards, power switch etc. and speakers. 

-  43” full HD 1080p IPS display, with 178° wide viewing angle
-  LED Backlight, picture-in-picture functionality
-  The inverter and the power supply can be reused with no modifications

What we don't need: 
-  Mirror Software: Android-based OS, proprietary launcher. Without any way to jailbreak this system, it isn't very useful to us. 
-  Camera: Unlikely to work post-modification. mipi csi interface, to get that to work for lulu required an entire team of engineers quite a bit of time and consideration in order to get that exactly how they wanted it.
-  The scalar board (with hdmi, usb and the antennas) would require reverse engineering the bios, very challenging. 

| Scalar Board front | Scalar board LVDS | Scalar board back | 
|------------|-------------|------------|
|<img src="https://github.com/olm3ca/mirror/blob/1236c9e7ffa5e38db7e17624a2214aead6a7a62e/Mirror1.jpeg" width="300">| <img src="https://github.com/olm3ca/mirror/blob/fac28bf8ac4261a449fda05f3c602d53389d4e51/Mirror2.jpeg" width="300">| <img src="https://github.com/olm3ca/mirror/blob/fac28bf8ac4261a449fda05f3c602d53389d4e51/Mirror3.jpeg" width="300">|

### Hardware Versions
There are several hardware revisions made to the Mirror. 
- Mine is Rev08, ordered November 2022. Photos uploaded to this repo are my own.
- My Panel is a [BOE DV430FHM-NN5](https://www.panelook.com/DV430FHM-NN5_BOE_43_LCM_overview_48245.html) which is the same panel as this [HV430FHB-N10](https://www.panelook.com/HV430FHB-N10_BOE_43_CELL_overview_30568.html). The good news is, this panel is used in several TVs made by Vizio, ONN and Samsung.

Other models of the Mirror have different panels: 

-  Many users have a Samsung LTI400HN01 [full specs](https://www.panelook.com/LTI400HN01_Samsung_40_LCM_parameter_31646.html) and [datasheet](SMSNG41.pdf) connected via LVDS
-  Some users have the [LM40SAMFHD700AG25WV Panel](https://www.panelook.com/LM40SAMFHD700AG25WV-40-TFT-Liquid-Crystal-Display-module-with-LED-Backlight-unit-detail_155306.html) and [datasheet](https://www.panelook.com/upload/product/210800/202302093705.pdf)
- User r/themiggysmigs provided these photos: https://imgur.com/a/uST7AOL
- RevP1 User r/AYfD6PsXcndUxSfobkM9 photos: https://imgur.com/a/bHYqefX | https://imgur.com/a/3JF6CdK | https://imgur.com/a/gHpoa2T

### Method
What you'll need: A Phillips head screwdriver, TR10, TR6 screwdrivers, a replacement TV mainboard, and whatever device you want to control the new Mirror (such as a Rasperry Pi, chromecast, a computer, or anything else).  

To make the Mirror display other content, follow these steps:
- Use a Phillips head screwdriver to remove the 4 screws on the back of the Mirror (and the 4 securing the bottom stand, if used). 
- Unscrew the scalar board: TR10 - three screws connecting it to the plastic frame from the Mirror. Then, use a TR6 for five screws to remove the board from the plastic shield.
- Disconnect the LVDS cable from the scalar board and the panel.
- Disconnect the audio from the scalar board as well. The speakers will still be connected to power, but we'll connect them to the new mainboard for audio output.
- Replace the scalar board with the TR6 and TR10 screws.
- The BOE display will work with a TV mainboard from any HV430FHB-N10 television hardware. [A quick search on eBay](https://www.ebay.com/sch/i.html?_from=R40&_trksid=p2332490.m570.l1313&_nkw=HV430FHB-N10&_sacat=0) provides for many options. Note: you will want a mainboard that comes with LVDS Cable, Ribbon Cables, Power Switch Board and IR Remote if possible. The connector on the tconn board is an ffc, so you need a cable for that.
- Connect your new HV430FHB-N10 mainboard to the Mirror via LVDS to the panel, and audio as well. 
- Connect your device (pi, chromecast, etc) via HDMI.
- Replace all screws, turn Mirror on, test, and configure!


### Other Mirrors
(For other units with non-BOE panels.) We will need to circumvent the proprietary scalar board's LVDS connection by using a programmable TV board that is easily sourced online, and re-mapping the LVDS pins to reconfigure the Mirror's layout with our new board. 

### How to Repin 
This is a reference guide for how to go about discovering the LVDS pin layouts:

Now for a quick definition of terms so we're both speaking the same language. We'll refer to the following as...
- the connector that attaches to the screen as "panel side" connector and the square connector as "Board side" connector or simply "the housing".
- The twisted wires simply as "Twisted pairs"
- The black wires as grounds (This is an assumption, will update if discovered to have a different purpose after your testing)

Now, On to the pin assignment. What we're looking for: we will reference the datasheet for the programmable TV board linked above, or any other model you are using.

Where to start:
- Take the panel side connector and hold it with the same side up as it is when it is inserted into the panel, so the gold side of the pins is facing toward you. (the cluster of 6 black wires will be on the right) going left to right from 1 to 51, use the multimeter set to continuity mode to figure out what pin positions on the panel side map to the pins on the housing side.
- To keep us all on the same page, number the pins as such.

1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,47,51

2,4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40,42,44,46,48,50

- For the housing side, it should be viewed head on so you're staring right down the barrel of each pin, with the latch on the bottom. once again, the cluster of 6 black wires will be on the right.

1,3,5,7,9,11,13,15,17,19,21,23,25,27,29

2,4,6,8,10,12,14,16,18,20,22,24,26,28,30

- The panel side connector is more challenging, I'd recommend taping a sewing needle to the end of your probe to give you that finer tip. once you've got those mapped out, hit me back with the findings so i can perform a sanity check to make sure everything looks good, and if we've found the datasheet for the driver board you purchased by then i'll provide a diagram for how to remap the housing!

- Next, As far as the header housings go. it can be a challenge to try to move the pins around while some of the sockets are populated. It is advised to buy another housing so you can just move from one to the other. The best way to do this to ensure that the pins will fit is to read the side of your current housing to determine the manufacturer and model.

For the Samsung panel, we will need to remap the pins accordingly:

- For panel side 22, 23, 37 and 38: Note(3) Input mode 10bit setting & 8bit input E_Chanel : Keep Level ‘0’

`Pin No 22 / 37 Pull Up(3.3V) with 1.5k ohm resistor`

`Pin No 23 / 38 Pull Down(GND) with 1.5k ohm resistor`

- For panel side pin 45: page 16 of the datasheet, it's signal description is "LVDS_SEL (2)" the paranthesis indicate which note applies. Note(2) LVDS Option :

`High(3.3V) Normal NS LVDS format`
`Low(GND or N.C) JEIDA LVDS format`

The panel defaults to jeida, we need to set it to normal lvds (aka vesa). 

### Accessories:
Below are ideas of boards and other tools to consider for your Mirror project.

- A programmable TV board such as [this model](https://www.ebay.com/itm/126199255216)
- 3.3v regulators such as [this option](https://www.amazon.com/Pieces-AMS1117-3-3-4-75V-12V-Voltage-Regulator/dp/B08CDMZMDN/ref=sr_1_1_sspa). It is most likely that we are going to have to provide a 3.3v signal to a specific pin. sometimes the driver boards like the one you ordered provide a pin for such things, sometimes they don't. 
- 1.5K ohm Resistors such as [this option](https://www.amazon.com/EDGELEC-Resistor-Tolerance-Multiple-Resistance/dp/B07QK3LHL9?th=1). we will need to add some resistors in line for 4 of the wires. you'll need at least 4 resistors. The important thing to look for is the tolerance which will be represented as a percentage. We need precision, so get 1% tolerance.

END of current steps - progress ongoing... 


