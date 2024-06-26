moofpico, a clone of a2pico 2.x (aka A2retronet RP2040)

This is a mostly-clone of the 2.4 through-hole [a2pico pcb board](https://github.com/rallepalaveev/a2pico), mostly for use as an Apple II <-> SD card interface, with a few minor tweaks. Why use this instead of one of the other boards out there? Mostly: no (E(E))PROMs, no PALs, nothing that needs to be programmed outside of using the Pico's USB connection - and designed so that almost all of the parts can be pretty easily hand-soldered.

The [RPi Pico datasheet](https://datasheets.raspberrypi.com/pico/pico-datasheet.pdf) explains some aspects that aren't made clear in either the schematic or its board symbol:
- the `3V3` pin is 3.3V in *and* out from the Pi unit; it's used to power both the RPi itself and can supply 300mA to other circuitry. Normally it's generated internally from...
- the `VSYS` pin is the main system input voltage (accepts 1.8V-5.5V); in our case, we can power it either from the apple II +5V slot, or from...
- the `VBUS` pin is connected to the uUSB pin1 connector; it can thus be used to power the unit when the Apple II itself is off, and...
- in section 4.5 they explicitly note how you should combine multiple power sources (VSYS + Schottky). TBH, I'm not sure why the DIP switch is needed.
- You can reset the RPi by pulling `RUN` low, or power the unit down entirely by pulling `3V3_EN` low.

While I don't think I'm allowed to redistribute the MEM2061 uSD socket footprint/3D model, you can grab it from DigiKey's model page: https://www.digikey.com/en/models/9859612 (the SnapMagic one). I've used the KiCad schematic symbol, even though it only has 11 pins and not 12 (extra is just shield ground).

The dimensions for apple2 peripheral cards is defined in IIgs tech note #28, https://mirrors.apple2.org.za/ftp.gno.org/doc/apple/technotes/iigs/tn.iigs.028
