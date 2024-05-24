# Arduino Parking System

## Overview
This Arduino project implements a simple parking system that uses IR sensors to detect the presence of vehicles and a servo motor to control a barrier. The system also includes an LCD display to show the number of available parking slots.

## Components
- Arduino board (e.g., Uno)
- 2 IR sensors
- Servo motor
- LCD display with I2C interface
- Jumper wires
- Breadboard

## Code Explanation
The provided code controls the parking system. It uses two IR sensors to detect vehicles entering and exiting the parking area. A servo motor is used to control the barrier. An LCD display shows the number of available parking slots.

### Libraries Used
- `Wire.h` for I2C communication
- `LiquidCrystal_I2C.h` for the LCD display
- `Servo.h` for the servo motor

### Pin Configuration
- `IR1` sensor connected to pin 2
- `IR2` sensor connected to pin 3
- Servo motor connected to pin 4
- LCD display connected via I2C (default address 0x27)

### Variables
- `Slot`: Total number of available parking slots
- `flag1`, `flag2`: Flags to track the state of the IR sensors

### Setup Function
- Initializes the serial communication, LCD, IR sensors, and servo motor.
- Displays an initial welcome message.

### Loop Function
- Checks the state of the IR sensors.
- Controls the servo motor to open/close the barrier.
- Updates the number of available parking slots.
- Displays the number of available slots on the LCD.

### Disadvantages:- 
-The sensor does not see black color


### Creators:-
Waleed Ahmed Elsayed Mabrouk     

Ahmed Wael Ali Mohamed      

Sameh Mohamed Elsayed        

Kareem Elsayed Awad Allah     

Osama  Abdelrahman Ebrahim       

 Mostafa Adel Mostafa

