---
layout: post
title: Custom Made timer
subtitle: Showcasing a custom 3 button timer with display
published: true
tags: [SPI display, Object-Orientation, PCB Design, Microcontroller]
---

## Design - Showcase


#### PCB Design 

I am still a relative new comer in pcb design so please don't hurt me. I have been using the rp2040 for a lot of different designs and it has a good hardware design document to go off of, so I decided to use it for the main controller for my board. The rest included some io to interface with an ST77- SPI adafruit display, an eeprom module, some buzzer io, battery charging stuff, 3 interface buttons, and some quality of life buttons. I copied most of the basics of the design from adafruits rp2040 board, but had an important change on the battery charging module. With adafruit's design, you cannot turn off power to the board while charging the battery. I considered this incompatible with my current project so I had to design around it.     



![schematic](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/pcb_schem.png?raw=true){: width="25%" :}schematic


![pcb-layout](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/pcb_layout.png?raw=true){: width="25%" :}layout



#### PCB Fabrication 

I ended up getting the pcb made from JLC pcb and most of the parts were placed with some soldered by hand by myself. I 3d printed the case and also tried out some 3d printed buttons while I was at it. 


![JLC-Output](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/IMG_7521_01.png?raw=true){: width="25%" :}Fresh From the Fab


![post-hand-solder](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/IMG_7537_01.png?raw=true){: width="30%" :}after hand soldered 




