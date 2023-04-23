# FlyingBear Ghost 6

This 3D printer is an affordable Core XY option. I documented my assembly steps with additional information to supplement the manual, this may help those looking to make upgrades.

![Front photo of FlyingBear Ghost 6 with a filament spool on the left](https://cdn.shopify.com/s/files/1/0589/7352/0045/products/01_f026b7af-a317-4852-a214-f21e87a4394c_1800x1800.jpg)

**Sections**

- [Motherboard](#motherboard)
- [Hot-end](#hot-end)
- [Z Stop](#z-stop)
- [PTFE Tube](#ptfe-tube)

[Nathan Builds Robots](https://www.youtube.com/@NathanBuildsRobots) posted a [review of this machine](https://www.youtube.com/watch?v=OnHAltxwU58), including some upgrades to the power connections and heat-break. I used this as a springboard of items to check when assembling my own Ghost 6.

## Motherboard

As of March 2023 FlyingBear appear to ship the Ghost 6 with fork connectors on the power cables, a welcome change from tinned wires as seen in NBR's review.

![A picture of the Ghost 6's motherboard showing the power cables screwed into terminal blocks with fork connectors installed](images/mks_terminals.jpg "Fork connectors installed from factory")

The motherboard is a [Makerbase Robin V3.1](https://www.makerbase.store/products/makerbase-mks-robin-nano-v3) (OEM Nano4 variant?) with four soldered stepper drivers and a socket to install an additional driver. The processor is a 32-bit single-core [STM32F407VET6](https://www.st.com/en/microcontrollers-microprocessors/stm32f407ve.html) running at 168Mhz.

![Overhead close up of the Makerbase Robin Nano V3.1 motherboard showing the STM32 processor, stepper drivers and UART pins next to the processor](images/mks_nano4.jpg)

This board ships running Marlin 2.x but also supports RepRapFirmware (RRF) and Klipper. Firmware images are available from the Makerbase [Nano V3 Github repository](https://github.com/makerbase-mks/MKS-Robin-Nano-V3.X#firmware).

## Hot-end

I dissembled the hot-end enclosure to inspect the heatsink and heat-break dimensions. This printer has a PTFE lined hot-end that runs down to the nozzle. As with other printers like the Ender 3, this limits the print temperatures to 240C as above this the PTFE tube burns.

The heat-break can be swapped out. It is a [Chimera](https://www.aliexpress.com/item/1005001728155269.html) style, M6 threaded bottom that screws into the heater block and a smooth J-head M7 throat that inserts into the cold-end heatsink (Aokin sell a cheaper [bi-metal TA-C smooth short](https://www.aliexpress.com/item/1005004234162702.html) variant).

![View of digital calipers and a de-installed cold-end heatsink on a desk, shown from the underside with the filament path visible where a heatbreak could be inserted](images/cold_end.jpg)

The heat-sink attachment to the yellow plastic hot-end enclosure appears bespoke. If you purchase an aftermarket alternative, you may need to drill and tap some M3 holes in the top of the heatsink near the perimeter to install it.

![Digital calipers showing a spacing of 12.34mm between M3 bolts screwed into the top of the aluminium cold-end heatsink either side of the filament path hole in the centre](images/heatsink_screws.jpg)

## Z Stop

I found my Z stop microswitch was not level from factory. This was easily remedied as it is mounted on a plate fixed with two bolts (circled in red), screwed into the rear panel of the frame.

![A view across the print bed showing the rear inside of the Ghost 6 where the Z stop switch is mounted between the Z axis lead screw and left hand side linear rod. The Z height stop position can be adjusted by rotating a ridged plastic cap mounted on a screw enclosed by a spring and washer](images/z_stop.jpg)

The Z stop plate bolts can be loosened from the rear of the machine.

![A picture of the rear of the Ghost 6, showing two bolt heads circled in red that adjust the level of the Z stop plate that micro switch is mounted on](images/adjust_zstop.jpg)

## PTFE Tube

When installing the PTFE tube from the frame edge to the extruder I checked the tube dimensions versus some Capricorn and Creality ender 3 tubing. The factory tubing appears to match Capricorn inner and outer dimensions.

![Three PTFE tubes held in pliers facing the camera end on, to compare the inner and outer diameters. Ghost 6 tube on the left, after-market Capricorn tube centre and Creality ender 3 tube on the right. The Creality tubing is noticeably larger in inner diameter](images/ptfe_compare.jpg)

This printer has a direct drive extruder, slack in tube's filament path before reaching the extruder does not affect print quality versus Bowden configurations where the PTFE tube sits between the extruder and hot-end.

## Next

I have some modifications planned and am yet to connect to the printer via serial over USB to pull the firmware settings. I'll update these notes in due course but am happy with the quality of the hardware, particularly at this price point.