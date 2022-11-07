Hardware not tested yet.

## Hardware
Features:
- IR interface for the [smart](https://youtu.be/aqHauk3bNFA) meter
- binary input for gas counter

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

## Links
- [3D model](https://a360.co/3Tq192N)  
- [Schematic](https://franz.science/stromzaehler/Schematic.pdf)  
- [iBom](https://franz.science/stromzaehler/ibom/)  
- [Tasmota](https://github.com/arendst/tasmota)