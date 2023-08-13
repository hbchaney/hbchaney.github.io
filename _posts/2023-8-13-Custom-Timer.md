---
layout: post
title: Custom Made timer
subtitle: Showcasing a custom 3 button timer with display
published: true
tags: [SPI display, Object-Orientation, PCB Design, Microcontroller]
---

## Design - Showcase


#### PCB Design 

I was asked to make a small timer and thought it would be a really cool project. I initially tried to do it modularly but found it too bulky and went with making a custom pcb. 

 I have been using the rp2040 for a lot of different designs and it has a good hardware design document to go off of, so I decided to use it for the main controller for my board. 
 
 The rest included some io to interface with an ST77- SPI adafruit display, an eeprom module, some buzzer io, battery charging stuff, 3 interface buttons, and some quality of life buttons. I copied most of the basics of the design from adafruits rp2040 board, but had an important change on the battery charging module. With adafruit's design, you cannot turn off power to the board while charging the battery. I considered this incompatible with my current project so I had to design around it.     



![schematic](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/pcb_schem.png?raw=true){: width="125%" :}


![pcb-layout](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/pcb_layout.png?raw=true){: width="75%" :}



#### PCB Fabrication 

I ended up getting the pcb made from JLC pcb and most of the parts were placed with some soldered by hand by myself. I 3d printed the case and also tried out some 3d printed buttons while I was at it. 


![JLC-Output](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/IMG_7521_01.png?raw=true){: width="75%" :}


![post-hand-solder](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/IMG_7537_01.png?raw=true){: width="75%" :}


![case-no-lights](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/IMG_7362.png?raw=true){: width="75%" :}

![case-intro-scene](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/IMG_7452.png?raw=true){: width="75%" :}

![case-running-timer](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/IMG_7456.png?raw=true){: width="75%" :}


#### Coding Note

I ran into huge bottlenecks with adafruits lib for interfacing with the display and had to make a variant of my own to get some decent frame rate. I took most of it from the PIO example from rasp pi's docs. 


#### Future Plans 

I plan on filling the empty space to the right with a tamagotchi style friend of some sort. 
