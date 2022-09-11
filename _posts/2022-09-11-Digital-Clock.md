---
layout: post
title: Digital Clock 
subtitle: Making a digital clock with a 7 segment display 
published: True
tags: [LED-Screen, Adafruit, Microcontroller, RP2040, Pico, Platformio]
---
## Hardware/Software - Showcase

### Overview  

![breadboard_digitalclock](https://github.com/hbchaney/Blogging/blob/master/Projects/Digital_clock/imgs/digital_clock_breadboard.jpg?raw=true){: width="50%" :}

I am making an alarm clock using the a .56" 7 segment display from adafruit with an RTC and light sensor as supporting peripherals. For user input, a Rotary Encoder with switch will be used. I plan to add in a buzzer/piezo in the future as well. 

### Functions 

I would like there to be a few features for this design:  
- regular clock*
- stop watch 
- alarm clock*
- timer 

** essential design elements 

### Code showcase 
To implement all these features, the rotary encoder will need to do a lot of work. it will need to have a way to cycle through numbers/ modes. and it will need a way to reset said modes and intiate the a way to cycle thorough the modes. 

Here is a sample of how a three input system for the switch part of the Rotary will work. 

---

    int RotaryEncoder::check_button() {  
    //5 for short press, 7 for long press of two seconds, 10 for press held down for more than 5 seconds 

    //short button press triggered on the release of  
    if (digitalRead(button_pin) == LOW && button_toggle == false) { //button pushed down and toggle not triggered yet (starts timer)
        press_start = millis(); 
        button_toggle = true; 
        return 0; 
    }
    else if (digitalRead(button_pin) == HIGH && button_toggle == true) { // button released timer reset
        button_toggle = false;
        if (two_second == true ) { 
            two_second = false; 
            return 0; 
        }
        else if (five_second == true) { 
            five_second = false; 
            return 0; 
        }
        else if (press_start + 25 < millis()) { 
            return 5; 
        }

    }
    else if (press_start + 2000 < millis() && button_toggle == true) { 

        if (two_second == false && five_second == false) { 
            two_second = true; 
            return 7; 
        }
        else if (press_start + 5000 < millis() && five_second == false) { 
            //reset the time and untoggle the button 
            two_second = false; 
            five_second = true; 
            return 10; 
        }

    }
    return 0; 
    }
--- 

more code [here](https://github.com/hbchaney/Blogging/tree/master/Projects/Digital_clock/Digital_clock)






