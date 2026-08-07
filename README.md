# Dino-s-auto
<img width="1060" height="760" alt="WhatsApp Image 2026-08-07 at 4 37 37 PM" src="https://github.com/user-attachments/assets/42e41e54-d025-403e-8e8c-7e24fcecd3f2" />

I automated the dino game on Google chrome with my Arduino uno a servo motor and an ldr 
# Demo
Watch Dino in action:- https://www.youtube.com/watch?v=lYSaGBG_zuU

# Overview
I wanted to use an ldr and a servo motor to automate the dinosaur game on google chrome.

# How it works
The Dino's auto uses an arduino uno micro controller, that connects to an ldr and a one 180 degree servo motor. The ldr sends an analouge signal to the arduino uno and if the signal is high enough (the screen is dark enough because of the obstacle in the dino's path) the arduino sends a high signal to the servo motor which moves to press the space bar so the dino jumps over the obstacle.

# Hardware 
This project consists of:
1) A arduino uno
2) LDR module
3) 180 servo motor
4) jumper wires
5) Usb A to B cable

### Bill of Materials (BOM)

| Component | Quantity | Exact Price (USD) | Purchase Link |
| :--- | :---: | :---: | :--- |
| ELEGOO UNO R3 Board (Arduino-Compatible) | 1 | $14.99 | [Amazon Listing](https://www.amazon.com/dp/B008GRTSV6) |
| SG90 Micro Servo Motor (5V) | 1 | $2.50 | [Adafruit Listing](https://www.adafruit.com/product/169) |
| LDR Light Dependent Resistor (Photoresistor) | 1 | $0.95 | [Adafruit Listing](https://www.adafruit.com/product/161) |
| Solderless Breadboard (400 Tie-Point) | 1 | $2.50 | [Adafruit Listing](https://www.adafruit.com/product/64) |
| Male-to-Male Jumper Wires (40-pack) | 1 | $3.95 | [Adafruit Listing](https://www.adafruit.com/product/758) |
| **Total Project Cost** | **—** | **$24.89** | — |

### Wiring Pinout Schedule

| Source Component | Source Pin | Target Component | Target Pin / Rail | Note |
| :--- | :--- | :--- | :--- | :--- |
| Arduino Uno | 5V | Breadboard | Positive Rail (+) | Main 5V power supply |
| Arduino Uno | GND | Breadboard | Negative Rail (-) | Common ground |
| LDR (Leg 1) | Terminal 1 | Breadboard | Positive Rail (+) | Direct 5V connection to LDR |
| LDR (Leg 2) | Terminal 2 | Arduino Uno | Analog Pin A0 (A0) | Direct connection to analog pin |
| SG90 Servo | Red Wire (VCC) | Breadboard | Positive Rail (+) | 5V power for servo motor |
| SG90 Servo | Brown/Black (GND) | Breadboard | Negative Rail (-) | Ground reference for servo motor |
| SG90 Servo | Orange/Yellow (PWM)| Arduino Uno | Digital Pin 8 (D8) | Servo PWM position control signal |

# Wiring diagram
<img width="1600" height="1453" alt="image" src="https://github.com/user-attachments/assets/8c86e52b-4628-476e-a33e-e8f387c42153" />



### Instruction manual
First tape the LDR to the screen of the monitor so that it sits just ahead of where your dino is on the screen.
Connect the LDR's GND to the Arduino's gnd and connect the LDR's vcc to the 5v pin on the Arduino.
Now connect the LDR's analog output pin to the A0 pin on the Arduino.
Connect the vcc and GND of the servo to the 5v and GND pin on the Arduino respectively 
Connect the signal wire to the Digital pin 8
Configure the code such that everytime the pixels on the screen turn dark because of an obstacle entering the Dino's path 
the arduino sends a high signal to the servo which pressed the space bar at judt the right time and voila.


# Programming
This project uses c++ as the only programming langauge. 
The IDE used is Arduino IDE.
The Board is an arduino UNO with a baud rate of 9600.
The primary method for choosing the threshold at which the uno sends a high signal to the servo is just trial error you should see what works best for you i personally used >330 
I the servo.h . It lets your board send precise pulse-width signals to position a motor at a specific angle without requiring you to write complex timer code.

# Code
#include <Servo.h>
Servo myservo;
int light;

void setup() {
  pinMode(8, OUTPUT);
  myservo.attach(8);
  Serial.begin(9600);
}

void loop() {
  light = analogRead(A0);
  if (light > 330) {
    myservo.write(90);
  }
  else {
    myservo.write(0);
  }
  Serial.println(light);
}
