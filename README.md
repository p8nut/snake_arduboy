# Snake ARDUBOY

## Requirements

- [Arduino IDE](https://www.arduino.cc/en/Main/Software)
- [Arduboy homemade package](https://github.com/MrBlinky/Arduboy-homemade-package)
- Some Motivation !

## Setup the tools

Install the arduino IDE and follow the steps of the arduino homemade package repository.

## Upload Configuration

In **Tools** select the following configuration:
* Board: "Homemade Arduboy"
* Based on: "SparkFun Pro Micro 5V - Standard wiring"
* Display: "SH1106"
* Bootloader: "original (Caterina)"
* Flash selected: "Pin0/D2/Rx"

## Hello World
Here is the HelloWorld which you can find in **File->Examples->Arduboy->HelloWorld**
 ```c++
/*
Hello, World! example
June 11, 2015
Copyright (C) 2015 David Martinez
All rights reserved.
This code is the most basic barebones code for writing a program for Arduboy.

This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.
*/

#include "Arduboy.h"

// make an instance of arduboy used for many functions
Arduboy arduboy;


// This function runs once in your game.
// use it for anything that needs to be set only once in your game.
void setup() {
  // initiate arduboy instance
  arduboy.begin();

  // here we set the framerate to 15, we do not need to run at
  // default 60 and it saves us battery life
  arduboy.setFrameRate(15);
}


// our main game loop, this runs once every cycle/frame.
// this is where our game logic goes.
void loop() {
  // pause render until it's time for the next frame
  if (!(arduboy.nextFrame()))
    return;

  // first we clear our screen to black
  arduboy.clear();

  // we set our cursor 5 pixels to the right and 10 down from the top
  // (positions start at 0, 0) 
  arduboy.setCursor(4, 9);

  // then we print to screen what is in the Quotation marks ""
  arduboy.print(F("Hello, world!"));

  // then we finaly we tell the arduboy to display what we just wrote to the display
  arduboy.display();
}
 ```
 
 Try to upload this code to your Arduboy.
 you must be able to read "Hello World" on your screen; if not call an **Assistant**
 
 ## First Draw Something
 
 in the [Arduboy header]()
 
 
 ```c++
#include "Arduboy.h"

Arduboy arduboy;

void setup() {
  arduboy.begin();
  arduboy.setFrameRate(60);
}

void draw() {
  arduboy.setCursor(4, 9);
  arduboy.print(F("Hello, world!"));
}

void loop() {
  if (!(arduboy.nextFrame()))
    return;

  arduboy.clear();
  draw();
  arduboy.display();
}
```
