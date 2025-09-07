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
