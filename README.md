#### Modified Anycubic Kobra Neo V1.33 Firmware

## Features
- Increased default extruder max feedrate from 25 to 50 (now retraction speed is not limited to 25mm/s)
- X and Y default max acceleration increased from 500 to 1000
- Default X and Y jerk increased from 5 to 8
- Enabled "Host Actions" and "Host Action Prompts" with support for the printer UI (allows starting/pausing/resuming of Octoprint prints)
- Increased probing accuracy by doing multiple probes per point
- Increased speed for the first Z-probe approach when double-probing
- Enabled quick home (X and Y homes at the same time)
- ~~Set default mainboard fan speed to 5 instead of 255~~ (reverted for now as I had a few "Heater_ID: 0 - Printer halted" errors)
- Enable M117 Gcode for setting messages to printer screen
- Enable M73 Gcode for setting progress bar on printer screen
- UI changes - black background, removed ugly yellow text color, fixed typos
- Added personal PID and E-Step values

## A note on Linear Advance and why it's not enabled
Unfortunately it seems that uncommenting #define LIN_ADVANCE is not enough to get linear advance to work properly with this version of Marlin and the Kobra Neo. While the feature itself works, there were issues with linear advance and TMC2208 drivers up until around mid 2022, causing the stepper to stall randomly during prints. [This PR](https://github.com/MarlinFirmware/Marlin/pull/24533) seemingly fixes the issue, but merging it to Kobra Neo fork causes weird wobbly stepper movement and prints that look awful. Other options include switching from stealthChop on the extruder to spreadCycle, but that causes the stepper to stall too, there's also SQUARE_WAVE_STEPPING but that reduces the stepper steps in half.

There is a fork of mainline [Marlin for HC32F46x MCUs](https://github.com/shadow578/Marlin-H32) (made to work on an Aquila X2), and I've got a base configuration done for Kobra Neo, but that fork currently does not have support for SoftwareSerial (which is needed for Kobra Neo's TMC2208 drivers that are running in UART mode) and TFT SPI (for our LCD display). Currently looking into it to see if I could port those features over.

## Download
https://github.com/jokubasver/Kobra_Neo/releases

## Flashing
Copy firmware.bin to your microSD card, insert the card with the printer off, turn printer on and wait until you get to the home screen. Afterwards, delete the firmware.bin file from your card.

## Before printing - reset your EEPROM
After flashing, I recommend to backup and reset your EEPROM (using the EEPROM Editor plugin in Octoprint), as I found that even after changing some values in the firmware, the printer still used the old values saved in EEPROM. After doing so, you will need to re-run auto bed leveing and set your Z offset again.

## Before printing - calibration

Perform a PID autotune and calibrate your e-steps! This firmware contains values for my own printer, but even the stock firmware does not have great values. 

Even after doing all the hardware and mechanical touch-ups, I was not getting great prints. This was solved by calibrating E-steps, as they were quite off (instead of extruding 100mm of filament, my printer extruded 95mm before calibration), so make sure you do that as well.

Instructions can be found here:

PID Autotune: https://teachingtechyt.github.io/calibration.html#pid

E-Step calibration: https://teachingtechyt.github.io/calibration.html#esteps

If you are building the firmware yourself, you can include your personal PID and E-step values in the firmware's Configuration.h file: https://github.com/jokubasver/Kobra_Neo/commit/a33ebd921d4031b541fb395de72f8292334ff8a0

Having these values saved in the firmware itself could save a lot of headaches, as If the EEPROM for whatever reason was to clear, your values will not dissapear.


## Building
https://www.reddit.com/r/anycubic/comments/y2waxu/tutorial_how_to_build_anycubic_marlin_source_code/

## Based on
https://github.com/sjorge/Kobra_Neo_Fw

https://github.com/jojos38/anycubic-kobra-improved-firmware

https://github.com/Auburn/Kobra_Go
