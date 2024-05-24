#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
#include <Servo.h> 

LiquidCrystal_I2C lcd(0x27, 16, 2);   
Servo myservo;

const int IR1 = 2;  // First IR sensor connected to pin 2
const int IR2 = 3;  // Second IR sensor connected to pin 3
const int maxSlots = 4; // Maximum number of parking slots available
int Slot = maxSlots; // Total number of parking slots available initially

int flag1 = 0; // Flag for the first IR sensor
int flag2 = 0; // Flag for the second IR sensor

void setup() {
  Serial.begin(9600); 
  lcd.init(); // Initialize the LCD
  lcd.backlight(); // Turn on the backlight

  pinMode(IR1, INPUT); // Set IR1 as input
  pinMode(IR2, INPUT); // Set IR2 as input

  myservo.attach(4); // Attach the servo to pin 4
  myservo.write(100); // Set servo to initial position (closed)

  // Display initial message
  lcd.setCursor(0, 0);
  lcd.print("     ARDUINO    ");
  lcd.setCursor(0, 1);
  lcd.print(" PARKING SYSTEM ");
  delay(2000);
  lcd.clear();  
}

void loop() { 
  if (digitalRead(IR1) == LOW && flag1 == 0) {
    if (Slot > 0) {
      flag1 = 1;
      if (flag2 == 0) {
        myservo.write(0); // Open the servo barrier
        Slot = Slot - 1; // Decrement the available slots
      }
    } else {
      lcd.setCursor(0, 0);
      lcd.print("    SORRY :(    ");  
      lcd.setCursor(0, 1);
      lcd.print("  Parking Full  "); 
      delay(3000);
      lcd.clear(); 
    }
  }

  if (digitalRead(IR2) == LOW && flag2 == 0) {
    flag2 = 1;
    if (flag1 == 0) {
      myservo.write(0); // Open the servo barrier
      if (Slot < maxSlots) {
        Slot = Slot + 1; // Increment the available slots
      }else{
         myservo.write(100);
         lcd.clear();
          lcd.print("slots are empty");
          delay(2000);
          lcd.clear(); 
      }
    }
  }

  if (flag1 == 1 && flag2 == 1) {
    delay(1000);
    myservo.write(100); // Close the servo barrier
    flag1 = 0;
    flag2 = 0;
  }

  // Display the number of available slots
  lcd.setCursor(0, 0);
  lcd.print("    WELCOME!    ");
  lcd.setCursor(0, 1);
  lcd.print("Slot Left: ");
  lcd.print(Slot);
}
