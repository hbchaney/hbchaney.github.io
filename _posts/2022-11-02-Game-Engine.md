---
layout: post
title: Creating a Game Engine for LED Cube
subtitle: Making a General object based game engine for the LED-Cube
published: true
tags: [LEDCube, Object-Orientation, framework, Microcontroller]
---

## Software - Walkthrough
<!-- image of snake in action -->

### Overview 

Games get complicated very quickly. Finding a way to ease the complexity is very important. I hope for the LED cube to one day have many available modes to switch to, and for each of those modes to have fleshed out interactive mechanics. 

To alleviate the complexity, I have developed an `Objects` based framework. Every `object` contains contains the values of their own coordinates and are responsible for creating a buffer of new values to be printed and old values to be erased. Printing of these `objects` and handling inter-object interaction is handled by a `mode` class. This `mode` class is responisble for passing values between `objects` and handling the printing of the `objects` to a display. 

A final `mode manager` switches between the `modes` and passes inputs into each `mode`. The `mode manager` also shows a mode preview and runs a `begin` function whenever a new `mode` is called. 

`Objects -> Modes -> ModeManager` 

### Loop Elements 

Many things need to be called in regular intervals. To ensure that a call gets made. I have designed a pure virtual class called `LoopElement`

This class has only one function that must be overridden `void Loop_check()`. An `Object`'s buffer functions are called in its loop checks at an interval determined by the `mode` that it exist in. 

```
class LoopElement { 

    public: 
    virtual void loop_check() = 0; 
};
```

### Objects 

The `Object` class looks like the following : 

```
class Object : public LoopElement
{
    protected:
    Coord display_buffer; 
    Coord off_buffer; 

    public:  
    uint16_t object_color;

    Object(); 
    
    Coord pull_display_buffer();  
    Coord pull_off_buffer();  

    //this game has a max of 1 pixel update and 1 pixel delete per frame for each object 
    virtual void update_display_buffer() = 0; 
    virtual void update_off_buffer() = 0; 

    virtual void loop_check() override;  //override from loop check 

};
```  

At the time of writing this `object` can only queue 1 pixel for creation and one pixel for deletion each frame. This is perfect for games like snake, pong, or brick breaker. The option might be added to utilize dynamic memory for the these buffers or have `object`s allocate more stack space to allow for more pixels to change per update. 

A later post will be made about how the `mode manager` functions with `modes`



