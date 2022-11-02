---
layout: post
title: Modular Design in FreeCAD
subtitle: Simplifying the 3d priniting design process using freeCAD
published: true
tags: [CAD, FreeCAD, modular Design, 3d printing]
---

## CAD - Showcase

### Overview  

While creating cases for the digital clock and LED cube, I went thorugh many iterations in CAD to get the parts to fit just right. This process involved me measuring then printing and exaiming the fit. Followed by more measuring and printing until the parts fit just right. 

This process is necessary, especially when you don't know the exact dimensions of the parts themselves, but becomes tedious when making a final combined design. 

To streamline this process I have come up with a way to more easily create designs in FreeCAD using a more modular approach. 

### Component Creation 

First a general component foot print needs to be established. To maximize modularity this foot print should not change much when established. 

Here is a look at some components 

![pico-slot](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/pico_slot.PNG?raw=true){: width="25%" :}microcontroller port 
![light-sensor](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/light_sensor.PNG?raw=true){: width="25%" :}light sensor 
![clock-face](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/clock_face.PNG?raw=true){: width="25%" :}clock face 
![rotary-encoder-slot](https://github.com/hbchaney/Blog_pictures/blob/master/Modular_freeCAD/Rotary_slot.PNG?raw=true){: width="25%" :}rotary encoder slot

### Case Creation 

Once the components are made and the foot prints are established, the case can be created and holes can be cut out where the components will be inserted

![case-cutout]()