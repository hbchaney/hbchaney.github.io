
---
layout: post
title: Custom Alarm Clock 
subtitle: From Concept to Finished Design
published: true
tags: [RP2040, Microcontroller, KiCAD, FreeCAD]
---

## Design Showcase 

![Finished Clock Picture](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/finished_clock.jpg?raw=true){: width="65%" :}

### Initial concepting 

I originally came up with the design by playing around with the pixel art software "aseprite". I wanted to create a modular general clock display and future controller for other projects. The design included eeprom, rtc, 
led display driver, battery charging, usb c, buzzer, rotary encoder with button, two tactile buttons, two seven segment displays. 

![aseprite concept](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/ClockConcept.png?raw=true){: width="65%" :}

### PCB design 

I was more conscious about designing around constraints than with past projects. I gave myself a more defined footprint that each part needed to fit in, and it resulted in a much better layed out pcb. I also favored more elegent routing that I could later adjust to in software for the led display driver. There are a few things I wished I aligned better, but overall I was pretty happy with the pcb design.

![Schematic picture](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/Schematic.png?raw=true)
![pcb screen shot](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/PCB_design.png?raw=true){: width="65%" :}  
![fabbed pcb picture](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/pcb_back.jpg.jpg?raw=true){: width="65%" :}  


### FreeCAD Design 

FreeCAD recently came out with a 1.0 version which was a great help with the design process. I was able to go back and adjust different parameters after the fact. In past versions, it was very frustating trying to change anything and usually resulted in starting designs over from scratch or stacking onto a bad design. I really love the new FreeCAD 1.0. I also was able to export the pcb and design around that and it made a huge difference to my work flow.

![front design](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/FrontFace_CAD.png?raw=true)  
![back design](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/BackFace_CAD.png?raw=true)  
![Assembled](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/Assembled_CAD.png?raw=true)

I was also able to laser cut acrylic for the front panel of the display and use tinting film to add more contrast.


### Software 

I built onto my previous software creations from past projects and also expanded a mode based heirarchal state machine. The software paradigm was modeled after a game engine, and I split all the peripherals to run on a dedicated core. This allowed for most of the tedious stuff to be abstracted away. 

I also had quite a bit of driver worked compared to previous projects. Initially, I was very unsure about creating my own drivers, but now that I have done it a bunch I feel much more confident in it. It greatly opens up the number of useable components because many of the libs out there are for outdated ICs. 

#### Mode Class

```
template <typename InputType, typename ModeTypeIndex>
class Mode 
{
    public: 
    Mode(ModeTypeIndex mode_type_in, std::function<void(ModeTypeIndex)> mode_switch_callback = [](ModeTypeIndex){}) : 
        mode_switch{mode_switch_callback}, 
        mode_type{mode_type_in}
    {} 

    virtual void process_input(InputType in) = 0; 
    virtual void tick() = 0; 
    virtual void exit_mode() {} //defaults to noop
    virtual void enter_mode() {} //defaults to noop
    ModeTypeIndex get_index() const {return mode_type; }

    protected: 
    std::function<void(ModeTypeIndex)> mode_switch; 
    const ModeTypeIndex mode_type; 

}; 
```

#### Update Class 
```
//will segfault if something dies 
//everything in update base should last the whole program 
class UpdateBase 
{
    private: 
    inline static unsigned int fix_freq = 1000; //for fix freq updates 
    inline static std::list<UpdateBase*> updates; 
    inline static std::list<UpdateBase*> updates_1; 
    inline static unsigned long last_update = 0; 
    inline static unsigned long last_update_1 = 0; 

    public: 

    UpdateBase(UpdateCore up_core = UpdateCore::CORE_0); //add to the updates list

    static void set_fixed(unsigned int freq) { fix_freq = freq; }
    static void run_inits(); 
    static void run_inits_1(); 
    static void run_updates(); 
    static void run_updates_1(); 
    static void run_fixed_updates(); 
    static void run_fixed_updates_1(); 

    //need to be defined
    virtual void init(); //common init function
    virtual void update(); 
    virtual void fix_update(); 

}; 
```


### Conclusion 

Overall I am very happy with the design. I still need to add a few more modes, but the current state is very usable. 

![Preassembled](https://github.com/hbchaney/hbchaney.github.io/blob/master/assets/img/alarm_clock/alarm_side.jpg.jpg?raw=true){: width="65%" :} 