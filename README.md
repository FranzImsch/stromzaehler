## Hardware
Features:
- IR interface for a [smart (DE)](https://youtu.be/aqHauk3bNFA) electricity meter,
- binary input for a gas meter (impulse counter),
- high efficiency buck converter for the USB power supply.

![Overview](assets/photo.jpg)  

The interface is mounted to the electricity meter using a ring magnet (27 x 5 x 16 mm). The magnet is glued into the 3D-printed [plastic part](https://github.com/FranzImsch/stromzaehler/blob/main/plastic_mount.step) as shown in the picture below.

A [threaded insert (M2)](https://www.digikey.de/en/products/detail/tri-star-industries-inc/M20X157C/13535373) is melted into the plastic piece so that the PCB can be mounted using an M2x5 screw.
![Cross section](assets/cross_section.png)
Detailed overview: https://a360.co/3Tq192N

Some electricity meters send data without 'request' and therefore the IR-LED along with its circuitry can be omitted in those cases. The [Volkszähler (DE)](https://wiki.volkszaehler.org/hardware/channels/meters) site is pretty useful to find information about different meters.

## Software
For Tasmota to use the SML feature, the following must be added to the ```user_config_override.h```-File (as per [documentation](https://tasmota.github.io/docs/Smart-Meter-Interface/)):

```
#ifndef USE_SCRIPT
#define USE_SCRIPT
#endif
#ifndef USE_SML_M
#define USE_SML_M
#endif
#ifdef USE_RULES
#undef USE_RULES
#endif
```
The software is compiled using the 8M tasmota32 preset. Flashed using [this](https://github.com/FranzImsch/CP2104-M8) serial adapter.

As soon as the device is connected to WiFi, the script for the electricity meter can be entered into the console (as per [documentation](https://tasmota.github.io/docs/Smart-Meter-Interface/#iskra-mt-681-sml)). The RX (25) and TX (26) GPIOs have to be adjusted. The script might need to be adjusted for the very meter that is used. For that, [this](https://tasmota-sml-parser.azurewebsites.net/) tool was tremendously helpful.

The **gas meter** is read with a reed contact. IO27 is set as a counter in Tasmota. What 1 Tick corresponds to in terms of gas is usually written somewhere on the meter. The counter is debounced using the [```CounterDebounce 250```](https://tasmota.github.io/docs/Commands/#sensors) command (which corresponds to 250 ms debounce time).

Also, the TelePeriod was set to 10 seconds (the fastest) as per [documentation](https://tasmota.github.io/docs/Commands/#mqtt).

## Links
- [3D model](https://a360.co/3Tq192N)  
- [Schematic](https://franz.science/stromzaehler/KiCad-Files/Schematic.pdf)  
- [iBom](https://franz.science/stromzaehler/ibom/)  
- [Tasmota](https://github.com/arendst/tasmota)