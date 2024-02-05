# I²C Slave driver for the RP2040 (Raspberry Pi Pico)
The single file in this repo is a ¿library? (maybe just a snippet,
really) to use the raspberry pico as a I²C slave device.

The target interpreter is MicroPython (tested on rp2-pico-20230426-v1.20.0 only).

So far it supports only:
- 7-bit addresses
- Single byte reads (blocking)
- Single byte writes (blocking)
- Multi-byte reads (blocking)
- Multi-byte writes (blocking)

It does **NOT** support:
- Interrupts/callbacks
- IRQs
- RPC
- 10-bit addresses
- Transactions
- Any other weird stuff.

The use of DMA is planned future work [(Blizzard) Soon™](https://wowwiki-archive.fandom.com/wiki/Soon).

The interrupts are NOT planned as future work due to Python limitations.
If at some point in time I learn how to wrap pycode around C and make it work nicely within/from Thonny (or any other blockhead-proof IDE), I might consider doing something... nevermind.

The development is based on the 2023 RP2040 datashet
- Build date: 2023-03-02
- ae3b121-clean

Is under MIT license so please feel free to contribute and try not to bug me about glitches, errors, bugs, and that kind of nasty stuff. PRs are more than welcome.

# Testing
The driver can be tested *standalone* with the following wiring:
- Connect GPIO0 to GPIO2
- Connect GPIO1 to GPIO3
- Connect VBUS to either GPIO0 or GPIO2 via a 18K resistor
- Connect VBUS to either GPIO1 or GPIO3 via a 18K resistor

Then plug to USB and enjoy on `/dev/ttyACM0`.

Any resistor of 10K or greater will do.
18K is the recommended value, but you can use any other one you have at hand.
These are necessary because, unlike the Raspberry Pi, the Pico doesn't have built-in pull-up resistors.

**It won't work without pull-up resistors**

The script will put both cores to work.
Core0 manages the slave while Core1 controls the master.
1. The Master generates two random integers that are sent to the Slave.
2. The Slave adds up the numbers.
3. The Master reads the result from the Slave.
4. Rince and repeat... forever.
