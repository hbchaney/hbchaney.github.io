---
layout: post
title: Creating a Game Engine for LED Cube
subtitle: Making a General object based game engine for the LED-Cube
published: false
tags: [LEDCube, Object-Orientation, framework, Microcontroller]
---

## Design - Showcase


#### PCB Design 

I am still a relative new comer in pcb design so please dont hurt me. I have been using the rp2040 for a lot of different designs and it has a good hardware design document to go off of, so I decided to use it for the main controller for my board. The rest included some io to interface with an ST77- SPI adafruit display, an eeprom module, some buzzer io, battery charging stuff, 3 interface buttons, and some quality of life buttons. I copied most of the basics of the design from adafruits rp2040 board, but had an important change on the battery charging module. with adafruits design you cannot turn of power to the board while charging the battery. I considered this imcompatable with my current project so I had to design around it.   

