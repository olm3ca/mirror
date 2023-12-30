## Creating a Smart Mirror from a Lululemon Mirror
Now that the company has started to abandon the product, it's time to open it up and make it a more functional smart mirror.

--------------------------------------------------------------------------------------------------------------------------------------------------------
### Before you begin, 
**By continuing, you acknowledge that you have read and understood the contents of the following disclaimer, and consent to their terms.**

**The process described in this document could cause irreversible damage to your Mirror, and you should prepare yourself for that outcome before you begin. I accept absolutely no responsibility for the consequences of anyone choosing to follow or ignore any of the instructions in this document, and make no guarantees about the quality or effectiveness of the software in this repo.**

--------------------------------------------------------------------------------------------------------------------------------------------------------

## Table of Contents

- [Hardware Notes](#hardware-notes)
- [Versions](#versions)
- [Hardware-based Solution](#hardware-based-solution)
- [Steps to Repin LVDS](#steps-to-repin)

--------------------------------------------------------------------------------------------------------------------------------------------------------

### Hardware notes:
We will be able to keep the same psu, backlight inverter, control boards (volume buttons, power switch etc.) and speakers. 
-  43” full HD 1080p IPS display, with 178° wide viewing angle
-  Panel: Most users have a Samsung LTI400HN01 [full specs](https://www.panelook.com/LTI400HN01_Samsung_40_LCM_parameter_31646.html) and [datasheet](SMSNG41.pdf) connected via LVDS
-  Some users have the successor to the Samsung Panel [LM40SAMFHD700AG25WV](https://www.panelook.com/LM40SAMFHD700AG25WV-40-TFT-Liquid-Crystal-Display-module-with-LED-Backlight-unit-detail_155306.html) and [datasheet](https://www.panelook.com/upload/product/210800/202302093705.pdf)
-  LED Backlight, picture-in-picture functionality
-  Android-based OS, proprietary launcher
-  The inverter and the power supply can be reused with no modifications
-  The scalar board (with hdmi, usb and the antennas) would require reverse engineering the bios, very challenging
-  Camera: Unlikely to work post-modification. mipi csi interface, to get that to work for lulu required an entire team of engineers quite a bit of time and consideration in order to get that exactly how they wanted it.

| Scalar Board front | Scalar board LVDS | Scalar board back | 
|------------|-------------|------------|
|<img src="https://github.com/olm3ca/mirror/blob/1236c9e7ffa5e38db7e17624a2214aead6a7a62e/Mirror1.jpeg" width="300">| <img src="https://github.com/olm3ca/mirror/blob/fac28bf8ac4261a449fda05f3c602d53389d4e51/Mirror2.jpeg" width="300">| <img src="https://github.com/olm3ca/mirror/blob/fac28bf8ac4261a449fda05f3c602d53389d4e51/Mirror3.jpeg" width="300">|

### Versions
There are several hardware revisions made to the Mirror. 
- Mine is Rev08, ordered November 2022. Photos uploaded to this repo are my own.  
- User r/themiggysmigs provided these photos: https://imgur.com/a/uST7AOL
- RevP1 User r/AYfD6PsXcndUxSfobkM9 photos: https://imgur.com/a/bHYqefX | https://imgur.com/a/3JF6CdK | https://imgur.com/a/gHpoa2T

### Hardware-based solution
To make the Mirror function as an enhanced smart mirror, we will need to circumvent the proprietary scalar board's LVDS connection by using a programmable TV board that is easily sourced online, and re-mapping the LVDS pins to reconfigure the Mirror's layout with our new board. Here is what we will need:
- A programmable TV board such as [this model](https://www.ebay.com/itm/126199255216)
- 3.3v regulators such as [this option](https://www.amazon.com/Pieces-AMS1117-3-3-4-75V-12V-Voltage-Regulator/dp/B08CDMZMDN/ref=sr_1_1_sspa). It is most likely that we are going to have to provide a 3.3v signal to a specific pin. sometimes the driver boards like the one you ordered provide a pin for such things, sometimes they don't. 
- 1.5K ohm Resistors such as [this option](https://www.amazon.com/EDGELEC-Resistor-Tolerance-Multiple-Resistance/dp/B07QK3LHL9?th=1). we will need to add some resistors in line for 4 of the wires. you'll need at least 4 resistors. The important thing to look for is the tolerance which will be represented as a percentage. We need precision, so get 1% tolerance.

### Steps to repin 
This is a reference guide for how we went about discovering the pin layouts:

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


END of current steps - progress ongoing... 


