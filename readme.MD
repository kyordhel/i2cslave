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

