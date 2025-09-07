# arduino_pitch_clock

## Overview
MLB pitch clock made at home with an arduino.
This pitch clock simulates 3 rules + game control:

1) 30 seconds between batters
2) 15 seconds between each pitch with no runners on base
3) 18 seconds between each pitch with runners on
4) Reset button when the batter steps off, pitcher
steps off, Mound visits, injury timeouts, and
offensive team timeouts.

This design uses an arduino uno r3 and an LCD 16x2 (I2C)

-------------------------------------------------------------------------------------------

## Materials

- Arduino Uno
- LCD 16 x 2 (I2C)
- 4 PushButtons
  - 15 seconds
  - 18 seconds
  - 30 seconds
  - Reset
- Breadboard
- Resistors
  -  220Ω for LCD backlight LED
  -  10kΩ for push buttons (4x)
- Jumper Wires
- Potentiometer

-------------------------------------------------------------------------------------------

## Wiring

### Circuit View
<img width="1259" height="887" alt="Screenshot 2025-09-07 at 6 01 30 PM" src="https://github.com/user-attachments/assets/35871490-eec1-4298-a2ce-e903ac33aaf0" />
(Made w/ Tinkercad)

### Schematic View

<img width="1055" height="813" alt="Screenshot 2025-09-07 at 6 03 37 PM" src="https://github.com/user-attachments/assets/e475cc8a-ceee-415f-a34f-be648acbf242" />

-------------------------------------------------------------------------------------------

## Code

```
/*

Pitch Clock Logic:

first button: thirty(30) seconds
- timer beween batters

second button: fifteen(15) seconds
- timer between pitches with the bases empty

third button: eighteen(18) seconds
- timer between pitches with runners on

fourth button: reset button
- reset button used when the batter steps off, pitcher
steps off, Mound visits, injury timeouts, and
offensive team timeouts.

*/

#include <LiquidCrystal.h>

// LCD pins
LiquidCrystal lcd(12, 11, 5, 4, 8, 7); 

// Buttons
const int thrityButton = 13; 
const int fifteenButton = 10;
const int eighteenButton = 6;
const int resetButton = 3;

// variables
int countdownTime = 0; 
unsigned long lastUpdate = 0; 
bool running = false; 

void setup() {
  lcd.begin(16, 2);
  pinMode(fifteenButton, INPUT);
  pinMode(resetButton, INPUT);
  pinMode(eighteenButton, INPUT);
  pinMode(thrityButton, INPUT);
  lcd.clear();
}

void loop() {
  // Start 15s countdown
  if (digitalRead(fifteenButton) == HIGH) {
    countdownTime = 15;
    running = true;
    lastUpdate = millis(); // reset timer
  }

  // Start 18s countdown
  if (digitalRead(eighteenButton) == HIGH) {
    countdownTime = 18;
    running = true;
    lastUpdate = millis();
  }

  // start 30s countdown
  if(digitalRead(thrityButton) == HIGH) {
    countdownTime = 30;
    running = true;
    lastUpdate = millis();
  }

  // Reset countdown
  if (digitalRead(resetButton) == HIGH) {
    countdownTime = 0;
    running = false;
    lcd.clear();
  }

  // Countdown logic
  if (running) {
    unsigned long currentMillis = millis();

    if (currentMillis - lastUpdate >= 1000) { // update every 1 second
      lastUpdate = currentMillis;

      // Decrement first so all numbers including 1 and 0 show properly
      if (countdownTime > 0) {
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.print(countdownTime);
        countdownTime--;
      } else {
        // Countdown reached 0
        lcd.clear();
        lcd.setCursor(0,0);
        lcd.print("0"); 
        running = false;
      }
    }
  }
}
```
