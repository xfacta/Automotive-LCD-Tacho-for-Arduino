# Automotive LCD Tachometer for Arduino
## Digital and bargraph display of RPM

- AT Mega2560 and 3.5" 320x480 LCD display
- Tachometer
- Peak RPM
- Uses pulseIn , no interupts
- Large text and
- Bar style graphical meter
- Reversed direction of bar to pair with speedometer
- Rounding of RPM to 10's or 100's depending on range
- Dim on "lights" input
- Button to reset peak RPM
- Outputs shift light data via serial for external shift light (on another arduino)
- Offloaded sounds to external Leonardo Tiny - currently the Tacho doesnt emit any warning sounds


![Tacho](https://user-images.githubusercontent.com/41600026/235329704-6a54a9bf-f901-4835-ae28-00de2161cee2.PNG)


### Uses 
UTFT Libraries and some associated font files

Copyright (C)2015 Rinky-Dink Electronics, Henning Karlsen. All right reserved

web: http://www.RinkyDinkElectronics.com/

This is the ILI9481 display used

https://www.altronics.com.au/p/z6527a-3.5-lcd-tft-arduino-mega2560-shield/


### It is required to check and adjust

```
RPM_redline = 8000
RPM_yellowline = 6000
cylinders = 4
minimum_RPM = 500
```
The assumption is 4 stroke operation, for 2 stroke you could just double the number of cylinders.

### You can also set
- `Demo_Mode` = true or false for display of random values
- `Calibration_Mode` = true or false for display of some raw data like input frequency in Hz
- `Kludge_Factor` is a way of adjusting timing since all Arduino crystals will be slightly different

Pressing the button at startup also enters calibration mode.

Pressing the button during normal operation resets the Peak RPM value.
Currently there is only a crude long-press detection using delay, and some debouncing in hardware is assumed.

The shift light function is offloaded to another Arduino via serial so the other Arduino can also use the LED strip for other functions such as warning lights.
Only the `RPM_yellowline` to `RPM_redline range` is output, lower RPM values are ignored.

The sounds are offloaded to a Leonardo Tiny to avoid delays and allow one Tiny and speaker to service multiple other functions such as Speedo and Fuel/Temperature/OilPressure gauge warning sounds.

The dimming function works by changing to using light grey and dark grey instead of white and colours, since there is no backlight control on the LCD panel I used.
