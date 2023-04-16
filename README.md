#### Modified Anycubic Kobra Neo V1.33 Firmware

## Features
- Increase probing accuracy by doing multiple probes per point
- Increased speed for the first Z-probe approach when double-probing
- Enabled quick home (X and Y homes at the same time)
- Set default mainboard fan speed to 5 instead of 255
- Enable M117 Gcode for setting messages to printer screen
- Enable M73 Gcode for setting progress bar on printer screen
- UI changes - black background, removed ugly yellow text color
- Add personal PID and E-Step values

## Download
https://github.com/jokubasver/Kobra_Neo/releases

## Flashing
Copy firmware.bin to your microSD card, insert the card with the printer off, turn printer on and wait until you get to the home screen. Afterwards, delete the firmware.bin file from your card.

## Building
https://www.reddit.com/r/anycubic/comments/y2waxu/tutorial_how_to_build_anycubic_marlin_source_code/

## Based on
https://github.com/sjorge/Kobra_Neo_Fw
https://github.com/jojos38/anycubic-kobra-improved-firmware
https://github.com/Auburn/Kobra_Go
