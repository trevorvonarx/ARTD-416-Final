# -- Mario's Pulse --
### Trevor von Arx
## ARTD 416 Final Project

I wrote an arduino sketch that which is to be implemented and used with pulse sensor, which takes the pulse of the human it is attatched to and uses that data to propell mario forward in the original Nintendo Entertainment System game, Super Mario Bros. My ideas for this project were derived from my childhood facination with video games and speculation on how our humanity can be injected into it. My task was not to try and make the controlls better, or worse, but to experiment and observe the experience that my project creates. 

The program works by sending a signal to the keyboard, telling it to press the "right" key, which is mapped to the respective direction in the video game emulator. I used two controllers, a playstation 4 dualshock, and the arduino. An arduino UNO does not hold enough processing power to allow for keyboard interation capabilities, so I went with the Bluefriut Feather 32u4 board can can handle the job. Below I have proveded the program and documentation of the Feather board and pulse sensor.

---

![alt text](https://www.tumblr.com/blog/tvonarx#)

--- 

### Arduino Sketch

#include "Keyboard.h"

#define KEY_RIGHT_ARROW   0xD7

int PulseSensorPurplePin = 0;                  // Pulse Sensor PURPLE WIRE connected to ANALOG PIN 0

int LED13 = 13;                                // The on-board Arduino LED

int Signal;                                    // holds the incoming raw data. Signal value can range from 0-1024

int Threshold = 650;                           // Determine which Signal to "count as a beat", and which to ingore.


void setup() {

  pinMode(LED13, OUTPUT);                      // Pin that will blink to as heartbeat
  
  Serial.begin(9600);                          // Sets up Serial Communication at certain speed.
  
  Keyboard.begin();                            // Sets up keyboard communication.
  
}

void loop() {

  Signal = analogRead(PulseSensorPurplePin);   // Read the PulseSensor's value.
  
                                               // Assign this value to the "Signal" variable.
                                               
  Serial.println(Signal);                      // Send the Signal value to Serial Plotter.
  
  if(Signal > Threshold) {
  
                                               // If the signal is above "550", then "turn-on" Arduino's on-Board LED.
                                               
    digitalWrite(LED13, HIGH);
    
    Keyboard.press(KEY_RIGHT_ARROW);           // Presses right arrow on keyboard
    
    delay(10);                                 // Hold the key for one second
    
    Keyboard.releaseAll();                     // Release the key
    
    
  } else {
  
    digitalWrite(LED13, LOW);  
    
     delay(10);
     
                                               //  Else, the signal must be below "550", so "turn-off" this LED.
                                               
  } 
}

---
