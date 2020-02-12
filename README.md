# Snake ARDUBOY

## Requirements

- [Arduino IDE](https://www.arduino.cc/en/Main/Software)
- [Arduboy homemade package](https://github.com/MrBlinky/Arduboy-homemade-package)
- Some Motivation !

## Setup the tools

Install the `Arduino IDE` and follow the steps from the `Arduboy homemade package` repository.

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
 
 Try to upload this code to your Arduboy by clicking on this icon  ![alt text](./img/upload_button.png).
 you must be able to read "Hello World" on your screen; if not call an **Assistant**
 
 ## First Draw Something
 
 in the [Arduboy header](https://github.com/Arduboy/Arduboy/blob/master/src/Arduboy.h) you can find some functions that will help you to draw on the screen like:
 - [void drawPixel(int x, int y, uint8_t color);](https://github.com/Arduboy/Arduboy/blob/3c409fefbb8b9c1d71c24070a33389d0b56f1333/src/Arduboy.h#L78)
 - [void drawCircle(int16_t x0, int16_t y0, uint8_t r, uint8_t color);](https://github.com/Arduboy/Arduboy/blob/3c409fefbb8b9c1d71c24070a33389d0b56f1333/src/Arduboy.h#L86)
 - [void drawLine(int16_t x0, int16_t y0, int16_t x1, int16_t y1, uint8_t color);](https://github.com/Arduboy/Arduboy/blob/3c409fefbb8b9c1d71c24070a33389d0b56f1333/src/Arduboy.h#L101)
 - [void drawRect(int16_t x, int16_t y, uint8_t w, uint8_t h, uint8_t color);](https://github.com/Arduboy/Arduboy/blob/3c409fefbb8b9c1d71c24070a33389d0b56f1333/src/Arduboy.h#L104)
 - [void drawRoundRect(int16_t x, int16_t y, uint8_t w, uint8_t h, uint8_t r, uint8_t color);](https://github.com/Arduboy/Arduboy/blob/3c409fefbb8b9c1d71c24070a33389d0b56f1333/src/Arduboy.h#L119)
 - [void drawTriangle(int16_t x0, int16_t y0, int16_t x1, int16_t y1, int16_t x2, int16_t y2, uint8_t color);](https://github.com/Arduboy/Arduboy/blob/3c409fefbb8b9c1d71c24070a33389d0b56f1333/src/Arduboy.h#L125)
 - [void drawBitmap(int16_t x, int16_t y, const uint8_t *bitmap, uint8_t w, uint8_t h, uint8_t color);](https://github.com/Arduboy/Arduboy/blob/3c409fefbb8b9c1d71c24070a33389d0b56f1333/src/Arduboy.h#L131)
 - [void drawChar(int16_t x, int16_t y, unsigned char c, uint8_t color, uint8_t bg, uint8_t size);](https://github.com/Arduboy/Arduboy/blob/3c409fefbb8b9c1d71c24070a33389d0b56f1333/src/Arduboy.h#L143)

Please try them with the following template (edit only the **draw** function). 
 
```c++
#include "Arduboy.h"

Arduboy arduboy;

void setup() {
  arduboy.begin();
  arduboy.setFrameRate(60);
}

void draw() {
  // draw function code here
  // arduboy.drawRect(10, 10, 5, 9, 0xFF);
}

void loop() {
  if (!(arduboy.nextFrame()))
    return;

  arduboy.clear();
  draw();
  arduboy.display();
}
```
## Make it Move

From now on you can display some shape on the screen !

But there are still not moving ... Which is sad ...
Let's try to make them move.

Draw a shape and make it bounce on the border of the screen. you can use the varaibles **HEIGHT** and **WIDTH** to get the size of the screen.

Do not forget that you can use **globals variables** to save the positions of your objects entities.

```c++
#include "Arduboy.h"

Arduboy arduboy;
// save your entities positions here

void setup() {
  arduboy.begin();
  arduboy.setFrameRate(60);
}

void update() {
  // move entities here
}

void draw() {
  // draw your entities here
}

void loop() {
  if (!(arduboy.nextFrame()))
    return;
  
  update();
  arduboy.clear();
  draw();
  arduboy.display();
}
```

## Handle buttons

```c++
#include "Arduboy.h"

Arduboy arduboy;

// ball position
int x = WIDTH / 2;
int y = HEIGHT / 2;

void setup() {
  arduboy.begin();
  arduboy.setFrameRate(60);
}

void update() {
  if (arduboy.pressed(RIGHT_BUTTON) && (x < WIDTH)) {
    x++;
  }

  if (arduboy.pressed(LEFT_BUTTON) && (x > 0)) {
    x--;
  }

  if ((arduboy.pressed(UP_BUTTON)) {
    y--;
  }

  if ((arduboy.pressed(DOWN_BUTTON)) {
    y++;
  }
}

void draw() {
  // draw your entities here
  arduboy.drawRect(x, y, 5, 9, 0xFF);
}

void loop() {
  if (!(arduboy.nextFrame()))
    return;
  update();
  arduboy.clear();
  draw();
  arduboy.display();
}
```


## Make your own game

From now on you should be able to code any basic game with Adruboy !

 **HAVE FUN**
