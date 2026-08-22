# Reflow946

> **Fork notice** — This is a modified version of [Reflow946](https://github.com/DurandA/reflow946)
> by Arnaud Durand, licensed under the [Creative Commons Attribution 4.0 International
> license](LICENSE) (CC BY 4.0). See *Modifications* below for what changed.

The Reflow946 is a Bluetooth LE temperature controller for the 946C electronic hot plate. Using this controller, a reflow profile can be programmed from your web browser using the [Web Bluetooth](https://webbluetoothcg.github.io/web-bluetooth/) API. You can use preset profiles (e.g. for lead-free or leaded soldering) or create a custom profile for a perfect cheese fondue. 🫕

![UYUE-946C](https://github.com/DurandA/reflow946/wiki/images/UYUE-946C.png)

The controller board is intended to replace the original controller board. It is **only compatible with the 3 buttons variant** pictured above (see this [teardown](https://youtu.be/Gv2sRJ9y_Ok)). Please send a PR if you adapted the design to a new variant.

## Hardware

The controller is based on a ESP32 module with an IPEX antenna. Since the metal case acts as a Faraday cage, the BLE signal can be improved by taping an antenna outside of the case.

### Front

![PCB front](https://github.com/DurandA/reflow946/wiki/images/front.png)

### Back

![PCB back](https://github.com/DurandA/reflow946/wiki/images/back.png)

## Status

- [x] Temperature control
  - [x] Temperature control using the front panel
  - [x] [BLE GATT service](https://github.com/DurandA/reflow946-firmware/wiki/GATT-Services) for temperature control
- [x] Reflow profile programming
  - [x] [BLE GATT service](https://github.com/DurandA/reflow946-firmware/wiki/GATT-Services) for reflow profiles
  - [x] [Web Bluetooth application](https://duranda.github.io/reflow946/)

## Modifications

Changes by Trent Rand (Randware), relative to upstream rev 1.2:

- Pathfinder revision (rev 2): 3-digit 7-segment display (`DS1`, DNP) replaced by a
  1.47" IPS TFT (ST7789V3, 172x320) attached through pogo/header interface `J6`:
  3V3 / GND / CS(IO23) / DC(IO16) / RST(IO13) / SCK(IO18) / MOSI(IO19) / BLK(IO5).
  Former segment-drive GPIOs were repurposed; digit transistor Q3 + R19 are DNP.
- Second MAX31855KASA (`U6`) with screw terminal `J8` (`EXT_TC`) for top-of-PCB
  thermocouple profiling; shares CLK/MISO with the primary sensor, CS on IO4.
- Breakout `J7` (CLK / MISO / CS_EXT / TC_ADC / 3V3 / GND) for probe-amplifier
  experiments (MAX31856 or analog AD8495 on SENSOR_VP).
- I2C expansion bus retained on IO17/IO22 with R21/R22 pull-ups.

Upstream hardware errata and revision notes are preserved in [`hardware/README.md`](hardware/README.md).

## Credits

* Arnaud Durand - Original design ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/))
* Elías Rodríguez Martín - Revision 1.1, conversion to KiCad
* Trent Rand (Randware) - OLED display interface, external probe interface
