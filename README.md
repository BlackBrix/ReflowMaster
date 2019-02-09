this is a good firmware already,  
but is is technically not possible to do (fast) PWM on the DC-Input of a AC-SSR.  
AC-SSR's uses SCR/thyristor or TRIAC on the output and inherently switch off (by themselves) at the points of zero load current (if the control-iput is low),  
and typically they have a response time that is "0.5 cycle" + 1msec  ("1 cycle" is 20ms@50Hz [or 16,66ms@60Hz])  
Or to be more simple:   
you can switch ON a SSR intantly* with the control input but you can not switch it OFF again in the middle of a sine half wave (in each case it will switch OFF at the next zero crossing of the load current).  
  
*(when using SSR-Type "Instant-on switching" instead of Type "Zero switching")  
    
    
see here for reference: http://www.crydom.com/en/tech/newsletters/solid%20statements%20-%20ssrs%20switching%20types.pdf  
or here as well: https://www.gavazzionline.com/pdf/ssrbrochure.pdf
    
    
There are three possible ways to "modulate" [0..100%] the heating power of the reflow oven:  
  
1.) syncronizing the SSR switching with the mains frequency/phase (like every simple light dimmer does) [doing phase angle control]  
you can see very well here how this is done --> https://youtu.be/8Y5AxWws0tI    
  
2.) using a SSR with built in phase angle control - most of them have industrial standard analog inputs like 4..20mA or 0..10V, so you have to find a way to convert the 0..3,3V PWM of the reflow master into these industrial standard signals.
  
3.) Doing "slow PWM" with a period that is much slower than the mains sine wave ("1 cycle" is 20ms@50Hz [or 16,66ms@60Hz])  
since we are talking about a thermally very slow/inert system (the oven), it doesn't matter how slow it is...  
(tis is also called "Burst Mode" or "Full Cycle Switching" in the reference document listed above)
    
    
We are doing 3.) "slow PWM" here with 0,8 Hz (1275ms period),  
I will modify this firmware accordingly in the future (not started yet 2019-02-08)


----

# ReflowMaster

Reflow Master is my open source toaster oven reflow controller that I also sell full assembled on tindie:
https://www.tindie.com/products/13378/

![Reflow Master](http://3sprockets.com.au/um/projects/reflowmaster/Pict_01.jpg)

It's custom hardware and custom code but all open source so if you want the challenge of making one yourself or you want to hack the code, go for it!

I have a live stream build of the board here if you want to see what's involved
https://www.youtube.com/watch?v=OGQ-GZZ90oE


# ReflowMaster Design Files

Inlcluded in this reposity:
- EagleCAD schematics and Board layout files (Eagle 9.1) 
- Exported Gerber files (Gerber 274X)
- STL files for the 3D printed case
- Adrduino code

# Which TFT?
The TFT I am using is a 2.4" SPI TFT using the ILI9341 Driver available via...

AliExpress
http://s.click.aliexpress.com/e/bQYyZYRe

Ebay
https://rover.ebay.com/rover/1/705-53470-19255-0/1?icep_id=114&ipn=icep&toolid=20004&campid=5338252684&mpre=https%3A%2F%2Fwww.ebay.com.au%2Fitm%2F2-4-240x320-SPI-TFT-LCD-Serial-240-320-ILI9341-PCB-Adapter-SD-Card-M52%2F291549777432%3FssPageName%3DSTRK%253AMEBIDX%253AIT%26_trksid%3Dp2057872.m2749.l2649

# SAMD21 Bootloader
You will need to use a SAMD21G18 that already has an Arduino bootloader on it *before* it is put on the board. If you need to add a bootloader, you'll need an ATMEL ICE and an adapter for the chip. The cheapest adapter you can get is my SAMD21G Mangler available here...
https://www.tindie.com/products/13379/

# Hacking the code
The Reflow Master board works like an "Adafruit Feather M0" - so you'll need to have the Adafruit Cortex m0 hardware profiles installed as well as the regular Cortex m0 Arduino profiles.

![Reflow Master](http://3sprockets.com.au/um/projects/reflowmaster/Pict_03.jpg)

You can use the instructions here to install everything you need to get up and running in the Arduino IDE:
https://learn.adafruit.com/adafruit-feather-m0-basic-proto/setup

You will also need the following lobraries installed
- Spline library http://github.com/kerinin/arduino-splines
- MAX31855 library by Rob Tillaart https://github.com/RobTillaart/Arduino/tree/master/libraries/MAX31855

Plus the following libraries from Library Manager
- One Button
- Adafruit_GFX
- Adafruit_ILI9341
- FlashStorage
   
Enjoy!

# Buy me a coffee or back me on Patreon?
I love making and designing projects but sharing open source projects takes a lot of thought and time. I do it because I think it’s important to share knowledge and give back to the community like many have done before me.

If you find this project useful or want to see more open source projects like it, please consider buying me a coffee or backing me on Patreon to say thanks!

[![buymeacofee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/YLVGbhJP0)
[![patreon](http://3sprockets.com.au/um/PatreonSmall.jpg)](https://www.patreon.com/unexpectedmaker)

# Unexpected Maker
http://youtube.com/c/unexpectedmaker

http://twitter.com/unexpectedmaker

https://www.facebook.com/unexpectedmaker/

https://www.instagram.com/unexpectedmaker/

https://www.tindie.com/stores/seonr/

