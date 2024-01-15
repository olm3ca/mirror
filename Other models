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
