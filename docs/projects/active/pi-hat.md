# Pi Power Hat

We have been manufacturing 3.81mm CamCon to micro USB B cables and they consistently fail or break. For Smallpeice 2018 we attempting to make them more robust with [Sugru](https://sugru.com/), but this didn't help much and just made a huge mess.

The Pi Power Hat aims to inject 5V power directly into the header of the Raspberry Pi. It must contain the appropriate protection circuitry to do this.


## Revision 1

Revision 1 was designed by Jack Williamson in the run-up to Smallpeice 2019. 19 boards were manufactured.

This revision met all of the above requirements and proved robust in testing. It was successfully deployed at SP2019.

Additionally, indicator LEDs were added that show the status of the usercode running on the robot. This was shown to have a massive increase in UX for students and volunteers using the kit as it was clear immediately if the code broke.

### Issues

- The main issue with this revision is that one of the indicator LEDs was wired to the 5V UART TX Pin on the Raspberry Pi. This resulted in a bright green flickering light that we could not control.
- Additionally as the UART pins were covered, the serial console could not be used for debugging.
- A lesser issue was that the polarity on the Camcon was reversed to our convention.

## Revision 2

Revision 2 is currently in the design stages.

It aims to make the following improvements over the original design:

- Rewire LEDs to GPIO Pins without UART functionality.
- Correct the polarity on the Camcon
- Investigate using an RGB LED instead of three individual LEDs to provide more error colours.
- Investigate using a 12V Regulator onboard to reduce load on the 5V regulator on the power board.
- Investigate use of a I2C EEPROM such that it is detected by the Pi according to the [HAT Specification](https://github.com/raspberrypi/hats)
- Investigate exposing the UART for easier debugging.
  - This includes investigating the use of a USB-Serial chip (FTDI or similar).

Jack Williamson is currently heading up this project.
