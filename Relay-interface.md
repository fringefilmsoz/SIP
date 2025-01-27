# A simple DIY relay interface

***

## There is a new, easier port expader plugin

### Astrogerard has contributed an excellent plugin that allows for a large number is stations to be easily and inexpensively added to SIP.

### It is called "pcf857x_plugin" and is available from the SIP plugins repo through SIP's plugin manager page. It uses i2c and requires SIP to be running under Python 3.
***

If you don't mind a little soldering you can build this simple but reliable circuit to connect 5V relay boards to your Raspberry Pi. This works with SIP without any software modifications. The interface uses only 4 GPIO pins (plus one for power and one for ground) allowing you to connect other devices to your Pi.

There are only a few inexpensive conponents needed:
- 74HC595 Shift Registers
- a few pin headers
- some jumper wires
- a 10k Ohm resistor
- a 0.1 microfarad capacitor (optional)
- a bread board, perf board or other support

You can get them from most electronics parts suppliers. For example Adafruit sells a 3 pack of [74HC595 chips](https://www.adafruit.com/products/450) for $2.75.

The diagram below shows a breadboard layout that supports up to 24 stations.

![shift register layout](images/SIP_shift_register_layout.jpg)

Each 74HC595 shift register allows you to connect 8 relays. You can chain as many shift registers together as needed.

**Note:** This shift register interface can work with either active high (high level trigger) or active low (low level trigger) relay boards. If you are using an **active-low** relay board such as those from SainSmart you will need to check the **Active_Low Relay** box under **Station Handling** on SIP's **Options** page. This enables the proper output mode for active low boards. Be sure that all relay boards attached to this interface are of the same trigger type.

If you need to increase the number of stations that SIP displays you can do so by increasing the number of **Extension boards** also under **Station Handling**. 0 for 8 stations (the default), 1 for 16 station 2 for 24 stations etc.


If you will be using a large number of stations, especially if more that a couple of relays will be on at the same time, you should consider adding a separate power supply to run the relays.