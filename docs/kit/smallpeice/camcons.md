# Camcons

(also known as pluggable terminal blocks)

"Camcons" are the little green connectors we use for high-current (over 1A) wiring in robots kits. A major benefit is that the plugs have screw terminals, making attaching/detaching them to wires very convenient. The **male** connector is the **receptacle** on the board, and the **female** connector is the pluggable terminal block itself.

We mainly use three types, based on their pin count and _pitch_ (the distance between the pins):

* 2 pins, 7.5mm pitch
  * Used for the six 12V outputs on the power board, and the corresponding 12V input on the motor board.
* 2 pins, 5mm pitch
  * Used to connect motors to the motor board.
  * Also used for connecting an external power switch to the power board.
* 2 pins, 3.81mm pitch
  * Used for the two 5V outputs on the power board.
  * Also used for connecting an external start button to the power board.

The motor board's UART interface (an alternative to controlling it over USB) uses a fourth type: 4 pins, 3.81mm pitch. However, we don't currently make use of this feature in the kit.

Note that the female connectors are **not** symmetrical, and the retaining clips on the top of the block are offset to the left slightly. If you are assembling cases that these connectors must be inserted into, you will need to take into account the orientation of pieces that may look interchangeable but in reality are not due to these keyed clips.

![Camcon](/img/kit/smallpeice/camcon.jpg)

## Etymology

As far as I can tell, "camcon" is a completely made up name for what is formally a "pluggable terminal block" (which is [how Onecall refers to them][onecall-example], for example). My guess is that it's short for "Camdenboss connector", though Camdenboss make a plethora of other types of connector too.

[onecall-example]: http://onecall.farnell.com/-/-/-/dp/2493650
