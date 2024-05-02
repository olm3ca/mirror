## Instructions specific to Mirro with panel LM40SAMFHD700AG25WV

Initial work thanks to [@avitascmor](https://github.com/olm3ca/mirror/issues/8) 

These are notes compiled from other users in the Issues section for Mirrors with LM40SAMFHD700AG25WV panels. For more details, read Issues [#8](https://github.com/olm3ca/mirror/issues/8) and [#10](https://github.com/olm3ca/mirror/issues/10) for more in-depth discussion. 

Here is the [technical manual](https://m.panelook.cn/LM40SAMFHD700AG25WV-40-TFT-Liquid-Crystal-Display-module-with-LED-Backlight-unit-detail_155306.html)

This model requires a specific cable and controller: https://ebay.us/HkicYV

This controller and cable set work and provide VGA, DVI and HDMI inputs for a Pi, Laptop, etc.  One solution is to replace the LVDS cable and let the rest of the screen remain powered by design.

Photos:

https://imgur.com/gallery/e8AqDlA | With MagicMirror2 running on a Pi4 https://i.imgur.com/MrhZ6gI.jpeg

## Reset mode to enable backlight: 

1. Reset the Mirror to initial state through the app or by pressing the blue button if installed.
2. If you cannot complete the above step and the Mirror is connected to Wi-Fi, remove it from your network by either kicking it off from the router, changing the Wi-Fi password, or removing the RF cable connecting the Wi-Fi antenna to the mainboard (RF cable removal may be irreversible).

## More detailed build instructions: 

Build notes thanks to [@jeremy-fields](https://github.com/olm3ca/mirror/issues/10)

I pulled out the original microphone board, usb access, video board, and speaker amplifier. I installed the [new board](https://www.ebay.com/itm/166580220209?siteid=0&customid=lululemon&toolid=20012) from eBay, a Raspberry Pi 4, and some connectors. I left the camera board and lens installed to prevent an obvious hole visible from the front (could also tape it off but this was easy). I also left the Power Supply and Backlight Inverter in place.

Mounting the boards was a little bit of a challenge. I used two posts from the speaker amp and two 0.5" [sticky mounts](https://www.amazon.com/dp/B07F23656R?psc=1&ref=ppx_yo2ov_dt_b_product_details ) on the Pi. I had to mount the Pi to a [mounting board](https://www.amazon.com/dp/B07BX2BVWB?psc=1&ref=ppx_yo2ov_dt_b_product_details) first.  

I used 4 [shorter sticky mounts](https://www.amazon.com/dp/B0C7QQ97GG?ref=ppx_yo2ov_dt_b_product_details&th=1) (0.25") for the new monitor board. The LVDS cord length and PSU cord lengths limit placement.

I added a USB-A port to the top of the mirror for the Pi. There was a USB micro there originally, but I wanted something easy to plug into so I swapped it out with [this](https://www.amazon.com/dp/B00G6SOP3I?ref=ppx_yo2ov_dt_b_product_details&th=1). From where my Pi was mounted, I had to run a USB extension cord to it.

Since I only have one USB-A external connection, I bought [this hub](https://www.amazon.com/dp/B0BXWV79TK?ref=ppx_yo2ov_dt_b_product_details&th=1) to connect my keyboard and mouse to. It's nicer to be in front of the mirror when configuring it versus using VNC since the monitor is turned sideways (the mouse is hard on VNC). 

I drilled a 1" hole in the power/network/connector box in the right spot to add a USB-C connection for powering the Pi. I used [this bit](https://www.homedepot.com/p/Milwaukee-1-in-Hole-Dozer-Bi-Metal-Hole-Saw-with-3-8-in-Arbor-Pilot-Bit-49-56-9662/202327732) from Home Depot. I added [this part](https://www.amazon.com/dp/B0CDPTQDJ8?ref=ppx_yo2ov_dt_b_product_details&th=1) for a USB-C external port. They make [USB-C and USB-A combos](https://www.amazon.com/dp/B09TPC72Y9?psc=1&ref=ppx_yo2ov_dt_b_product_details), which I tried, but my drill hole was too small so I just used the USB-C bulkhead connector. It's pretty full down there, so maybe not a bad choice.

I was a little worried about the boards being so close to the cover so I added some Kapton type tape. Might be overkill. I chose [this](https://www.amazon.com/dp/B072Z92QZ2?psc=1&ref=ppx_yo2ov_dt_b_product_details) which came with way more than I needed.

The new board can power the backlight if you connect the wiring per the included instructions. I did that and was able to completely remove the old board. I wrapped all the new wires near the Power Supply with 80 degree C electrical tape. The original wires had a coating over them with 80C listed on it. I originally tried to power the video board through the power plug, but wiring it direct seems to be the better choice. I did have to move some pins around to get the plugs right. If you do this, pay attention to the +/- because the colors are not always correct - I found red wires connected to negative connections. 

The backlight is probably too bright for having this in the bedroom, so I bought a managed power outlet. I like the Kasa plugs so I bought [this](https://www.amazon.com/dp/B07B8W2KHZ?ref=ppx_yo2ov_dt_b_product_details&th=1). You can schedule it to turn on and off at certain times. 

Wi-Fi might be hard with the Pi inside, so I opted for a Ethernet connection. 
I haven't sorted out audio yet. The video board has audio connectors that are smaller than anything I pulled off, so pinning has been difficult. I did rig something up at one point, and it sounded good, but the wires don't really stay connected so I removed it for now. I might come back to it later.
The new video board came with a control board, but I removed it. You'd need to run it outside somehow and I don't think you really need it.

Now to figuring out how I want the software configured. 

Pictures: https://imgur.com/a/PxCpFC0

![New overview](https://github.com/olm3ca/mirror/assets/87494419/cc2112d8-aa69-4797-8176-29bfa287006e)

![Running 2](https://github.com/olm3ca/mirror/assets/87494419/f389971a-311f-4499-a1b0-c1c3160f2608)

Original power supply unit (PSU) setup. Power is going to the old mainboard and the microphone. There's also the Mirror's main on/off switch. I removed all of these, and unpinned the on/off switch for reuse on the new boards connectors. Some of these were hot glued down; I pulled the glue off and was able to disconnect.
![IMG_1753](https://github.com/olm3ca/mirror/assets/87494419/5ec2cb98-45c1-4f18-bf6f-5afb8bb141f3)

Top of the mirror; other end of the power cords. This is the old mainboard, camera, and microphone board. I removed everything, but then reinstalled the camera lens & board (no connections) so there's wasn't an obvious hole where the old camera and lens were. The mainboard receives power in a couple connections, with one of them double pinned to feed power out to the speaker board. I removed the speaker board as well (not shown - near PSU). I think that board is an amp and audio routing. I did try sound without it by temporarily wiring the speakers to the new board, and it worked fine, but I don't have a connector for connecting the speakers directly to the new board (I just rigged it for testing).
![IMG_1763](https://github.com/olm3ca/mirror/assets/87494419/4ab59eb8-85f9-498a-aa14-e088a0f502c0)

New board connected for testing. It's proving power to the TV/Monitor and backlight. TV/Monitor control button panel is wired but was later removed since there's no way to access these buttons from outside the mirror casing without a lot of work, and it wasn't really needed for this project. I may have used it to select input once - don't recall. Jumper cable versus power switch was still installed - see pic immediately following this one. You can replace that loop with the switch wiring, or leave it as-is and manage power with a smart switch or some other method. I liked the idea of having the switch wired, but in practice I have the power connected to a smart switch with a timer to turn the monitor & backlight on/off (on in the morning, off for bed).
![IMG_2040](https://github.com/olm3ca/mirror/assets/87494419/6fc514fc-c7b1-4ac1-91b9-672f7e28c7f3)
![IMG_2061 (1)](https://github.com/olm3ca/mirror/assets/87494419/87765a79-8a7e-40f2-98d1-15e0488a4697)

If you want to keep the switch, you can removed the cable from the old connector by depressing the tooth type metal bit, and pushing the pin & wire out from bottom of the connector. Once it was out, I pulled the teeth back up a little for better locking again in the new connector. Similar thing to remove the loopback cable, then insert the switch cords where the loopback was. Make sure you get the right holes since there's a bunch of empty pins there - I don't think color/polarity matters since you're just opening/closing a switch. 
![IMG_2060 (1)](https://github.com/olm3ca/mirror/assets/87494419/f71bb1e1-5a28-40b6-ad4f-f1e4d197cf8a)
![IMG_2063 (1)](https://github.com/olm3ca/mirror/assets/87494419/769a4d27-6d61-4690-b72e-5c9111d35485)

Completed project. I tried to route the cables to keep them from being too wild. Also, the original power cables were wrapped in 80°C jackets. New cables are not like that, so I used electrical tape with a similar rating and just wrapped the cords since they're running across the PSU. The Raspberry Pi is powered with its own cord.
![IMG_2138](https://github.com/olm3ca/mirror/assets/87494419/4813473e-7851-4af4-b31f-b3bc2cd7e303)

Hope this helps. Let me know if something isn't clear. Here's a bunch of related pics.
https://imgur.com/a/ztgrLKG

