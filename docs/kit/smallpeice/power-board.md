# Power Board

The power board is based on the open source [version 4 power board][sr-pb] originally developed by [Student Robotics][sr].


## Useful links

* [User-facing docs][docs]
* [Schematic PDF][schematic]
* [Hardware designs][hardware] (schematic, PCB and plastic case)
* [Firmware source code][firmware]

## Status LEDs

The power board has 9 LEDs that indicate the status of the board's subsystems.

* PWR|FLAT (DS1)
  * Off: 3.3V rail unpowered
  * Green: 3.3V rail powered 
  * Flashing orange and green: battery undervoltage detection tripped
    * Controlled by [`check_batt_undervolt`](https://github.com/sourcebots/power-v4-fw/blob/2795f9bd390fe409986ee1642762408a8a98edc8/main.c#L135).
* 5V (DS2)
  * Off: 5V rail unpowered
  * Green: 5V rail powered
* H0, H1, L0, L1, L2, L3 (DS3, DS4, DS5, DS6, DS7, DS8 respectively)
  * Off: corresponding power output is unpowered
  * On: corresponding power output is powered
* RUN|ERROR (DS9)
  * Off: board is either unpowered, initialising, or in an undervoltage or overcurrent alarm state
    * If unpowered, PWR|FLAT will also be off.
    * If in an undervoltage state, PWR|FLAT should also be flashing orange and green.
    * If in an overcurrent state, the buzzer should also be beeping.
    * Otherwise we can assume the board got stuck during initialisation, somehow.
  * Orange: initialisation complete, no USB connection or bus is reset
    * Both the green (RUN) and red (ERROR) elements are switched on in [`main`](https://github.com/sourcebots/power-v4-fw/blob/2795f9bd390fe409986ee1642762408a8a98edc8/main.c#L257) once `init` finishes.
  * Green: USB connected
    * The red (ERROR) element is switched off by [`set_config_cb`](https://github.com/sourcebots/power-v4-fw/blob/2795f9bd390fe409986ee1642762408a8a98edc8/pbusb.c#L322), leaving only the green (RUN) element on. `set_config_cb` is a callback that is called by low-level USB code as part of establishing a USB connection.
    * ERROR is switched back on if the USB bus is reset (i.e. USB disconnect), by [`usb_reset_callback`](https://github.com/sourcebots/power-v4-fw/blob/2795f9bd390fe409986ee1642762408a8a98edc8/main.c#L225).
  * Note that this LED can be controlled remotely - typically it is set to blink green while waiting for the user to press the start button

## How to compile and upload the firmware onto the board

1. Obtain and compile the [firmware][firmware].
    * `git clone --recursive git@github.com:sourcebots/power-v4-fw.git`
    * `cd power-v4-fw`
    * `make`
    * This should produce a file named `pbv4.bin`.
1. Plug a USB-to-serial cable into the 6-pin header in the corner of the board, and into your computer.
    * See the [pinout](#Serial-port-pinout) below.
    * Check that a serial device (e.g. `/dev/ttyUSB0`) appears when you plug the cable in.
1. Install [stm32flash][stm32flash].
1. Use the `pbv4-flash-fw` script from the [tools repo][tools] to flash the firmware onto the board.
    * `git clone --recursive git@github.com:sourcebots/tools.git`
    * `tools/bin/pbv4-flash-fw /dev/ttyUSB0 PBV4_BIN SERIALNUMBER`
        * Replace `PBV4_BIN` with the path to `pbv4.bin` that you compiled in the first step.
        * Replace `SERIALNUMBER` with the board's serial number.

[stm32flash]: https://sourceforge.net/p/stm32flash/wiki/Home/

### Serial port pinout

The mapping of pin numbers to signal names for the 6-pin programming header in the corner of the board is given below. If you are using a [C232HM][c232hm] USB-to-serial cable, the colour of the breakout wires corresponding to each signal is also listed.

| Pin number | Pin location          | Signal                 | [C232HM][c232hm] wire |
|------------|-----------------------|------------------------|-----------------------|
| 1          | in corner of board    | ground                 | black                 |
| 2          |                       | `CTS`                  | brown                 |
| 3          |                       | no connection          | red (optional)        |
| 4          |                       | board `RX` / host `TX` | orange                |
| 5          |                       | board `TX` / host `RX` | yellow                |
| 6          | next to the L1 socket | `RTS` (`BOOT0`)        | green                 |

[c232hm]: http://www.ftdichip.com/Products/Cables/USBMPSSE.htm

## How the board works

It is helpful to have a copy of the [schematic][schematic] handy when reading this section.

### Schematic page 2: the 12V supply

Note: the so-called "12V" supply is just the battery voltage, and therefore can actually range between 9.0V and 12.6V depending on the level of charge of the battery.

* Power source: a three-cell lithium polymer [[battery|Battery]].
  * Voltage is nominally 11.1V, but can vary between 9.0V and 12.6V depending on the charge level.
  * Battery can supply 44A continuous, 66A peak.
* Battery cable:
  * One end is bolted to the power board at connectors J1 (positive) and J3 (negative).
  * Other end presents a male XT60 connector, to which a replaceable battery can be connected.
* 40A fuse (F1):
  * This is not user-replaceable, but is serviceable by us.
  * This exists as a hard fallback to the 30A current limit enforced by the firmware, and as such rarely fails.
* Reverse polarity protection:
  * Consists of the parallel n-channel MOSFETs Q1 and Q2 ([IRFH5301 datasheet][IRFH5301]), the Zener diode D2 ([PESD5Z12 datasheet][PESD5Z12]) and the resistor R5.
  * Under normal polarity, current flows through Q1/Q2 from source (pins 1-3) to drain (pins 5-8).
    * This current flow is initially through the implicit body diode of each MOSFET, the anode of which is the MOSFET's source and the cathode is the MOSFET's drain.
    * The body diode creates a forward voltage drop of 1.0V, meaning it is relatively inefficient at conduction. However the current passed by it is is sufficient for R5 and D2 to pull the gates of the MOSFETs sufficiently above the threshold voltage to form a channel in the MOSFETs (i.e. turn them on).
    * This channel is a much better conductor, with resistance in the range of milliohms.
  * Under reverse polarity, the MOSFET body diodes are reverse-biased and the gates are not held above the threshold voltages, so no current may flow.
* Current sense:
  * The full battery current is passed through a parallel combination of the resistors R1 and R2.
  * The voltage across these resistors is fed to an INA219 current/power sensor ([datasheet][INA219]).
  * The INA219 provides a digital output, communicating the measurements to the microcontroller over [I²C][I2C].
* After passing through all of these protective circuits, the current from the battery is distributed across the 12V supply rail, named `VBATT` in the schematic.

[IRFH5301]: https://www.infineon.com/dgdl/irfh5301pbf.pdf?fileId=5546d462533600a40153561b477b1ebe
[PESD5Z12]: https://assets.nexperia.com/documents/data-sheet/PESD5ZX_SER.pdf
[INA219]: http://www.ti.com/lit/ds/symlink/ina219.pdf
[I2C]: https://en.wikipedia.org/wiki/I%C2%B2C

### Schematic page 3: the 3.3V and 5V supplies

* `VBATT` is fed through the internal and external power switches (in series) to produce the `VBATTSW` net.
  * This means `VBATT` is high even when the robot is "switched off", so long as a battery is plugged in.
* 3.3V supply:
  * A regulated 3.3V supply is derived from `VBATTSW` using a [buck converter][buck-converter] based around U2, a TPS62125 IC ([datasheet][TPS62125]).
  * The 3.3V regulator is turned on when the battery voltage rises above a threshold of 11.1V, and turned off when it falls below 9.6V.
    * A detailed explanation of how and why this is implemented is presented inline in the schematic.
  * The 3.3V supply powers the microcontroller and associated digital circuitry, and is not exposed as an output of the board.
* 5V supply:
  * Similarly, a regulated 5V supply is derived from `VBATT` (not `VBATTSW`) using a buck converter, this time using a TPS54327 ([datasheet][TPS54327]).
  * The 5V supply is turned on only when directed to do so by the microcontroller (the `5VEN` signal).
  * The 5V supply is not used within the board, but is exposed on two 3.81mm [[Camcons]].
    * In typical usage within our kit, this supply powers the Raspberry Pi (and thus all of its USB-connected devices e.g. webcam, arduino), and the servo shield.
  * Another INA219 (U4) is used to measure the total current through the 5V connectors.

[buck-converter]: https://en.wikipedia.org/wiki/Buck_converter
[TPS62125]: http://www.ti.com/lit/ds/symlink/tps62125.pdf
[TPS54327]: http://www.ti.com/lit/ds/symlink/tps54327.pdf

### Schematic page 4: 12V power outputs

* The 12V power outputs are switched by four VND5012 dual-channel power MOSFETs.
* Each of the four low-current 12V outputs is driven by one of the two channels in a VND5012.
* Each of the two high-current 12V outputs is driven by both channels of a VND5012 connected in parallel.
* The `OUT{H0,H1,L0,L1,L2,L3}EN` signals control whether each output is connected to or disconnected from the `VBATT` rail.
* The VND5012s have built-in current measurement, in the form of an analogue output per channel. An additional signal `CS_DIS` controls whether these outputs are driven or tri-stated by the VND5012.
  * To save pins on the microcontroller, the current sense signals from the four VND5012s are multiplexed in time.
  * Each VND5012 has its `CS_DIS` pin connected to a digital output of the microcontroller. At any time, one of the four `CS_DIS` pin is low (enabling the corresponding IC's current output) while the other three are high.
  * The [`current_sense_poll`][fw-current_sense_poll] function, [called frequently][fw-current_sense_poll-call] as part of the microcontroller's main loop, switches to activating the next `CS_DIS`.
  * The `CS0` and `CS1` pins are shared between the 4 VND5012s, but because only one `CS_DIS` is held low at a time, there is no contention on these pins.
  * `CS0` and `CS1` are wired to ADC inputs `PA0` and `PA1` on the microcontroller.

[fw-current_sense_poll]: https://github.com/sourcebots/power-v4-fw/blob/2795f9bd390fe409986ee1642762408a8a98edc8/output.c#L97
[fw-current_sense_poll-call]: https://github.com/sourcebots/power-v4-fw/blob/2795f9bd390fe409986ee1642762408a8a98edc8/main.c#L262

### Schematic page 5: microcontroller

TODO

## To do

* What job(s) does this board serve in the kit?
* What connectors/LEDs/notable features does it provide?
* How does this board behave in practice? (e.g. what failure conditions does it detect and how does it notify the user of them?)
* How does the board work?
* Bill of materials and assembly info

[sr]: https://studentrobotics.org/
[sr-pb]: https://studentrobotics.org/docs/kit/power_board
[docs]: http://docs.sourcebots.co.uk/kit/power-board/
[schematic]: http://docs.sourcebots.co.uk/docs/power-schematic.pdf
[hardware]: https://github.com/sourcebots/power-v4-hw
[firmware]: https://github.com/sourcebots/power-v4-fw
[tools]: https://github.com/sourcebots/tools
