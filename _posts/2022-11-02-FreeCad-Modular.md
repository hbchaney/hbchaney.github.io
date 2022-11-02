---
layout: post
title: Modular Design in FreeCAD
subtitle: Simplifying the 3d priniting design process using freeCAD
published: true
tags: [CAD, FreeCAD, modular Design, 3d printing]
---

## CAD - Showcase

### Overview  

While creating cases for the digital clock and LED cube, I went through many iterations in CAD to get the parts to fit just right. This process involved me measuring then printing and exaiming the fit. Followed by more measuring and printing until the parts fit just right. 

This process is necessary, especially when you don't know the exact dimensions of the parts themselves, but becomes tedious when making a final combined design. 

To streamline this process I have come up with a way to more easily create designs in FreeCAD using a more modular approach. 

### Component Creation 

First a general component foot print needs to be established. To maximize modularity this foot print should not change and should be a little oversized to be safe.

Here is a look at some components 

![pico-slot](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/pico_slot.PNG?raw=true){: width="25%" :}microcontroller port 
![light-sensor](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/light_sensor.PNG?raw=true){: width="25%" :}light sensor 
![clock-face](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/clock_face.PNG?raw=true){: width="35%" :}clock face 
![rotary-encoder-slot](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/Rotary_slot.PNG?raw=true){: width="25%" :}rotary encoder slot

### Case Creation 

Once the components are made and the foot prints are established, the case can be created and holes can be cut out where the components will be inserted

![case-cutout](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/Clock_cutout.PNG?raw=true)

A case is made with slots cutout for each component 

![assembled-case](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/Clock_assembled.PNG?raw=true)

The case is then assembled to yield the final product to be printed. 

### Conclusions  

This modular design method has really helped me not get burned out remeasuring things once I have an effective design. In the past, I was going back and using the measuring tool in FreeCAD on my old component iterations then putting them in a massive final design. Adding all that to the Heirarchy made things hard to change. This assembly based method is a much better approach and allows for components to be more easily swapped out. 