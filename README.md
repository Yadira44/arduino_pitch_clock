# arduino_pitch_clock

## Overview
MLB pitch clock made at home with an arduino.
This pitch clock simulates 3 rules + game control:

1) 30 seconds between batters
2) 15 seconds between each pitch with no runners on base
3) 18 seconds between each pitch with runners on
4) reset button when the batter steps off, pitcher
steps off, Mound visits, injury timeouts, and
offensive team timeouts.

This design uses an arduino uno r3 and an LCD 16x2 (I2C)
