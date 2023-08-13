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



![schematic](https://github.com/hbchaney/Blog_pictures/blob/master/Marianne_timer/Screenshot%202023-08-13%20111649.jpg)schematic
