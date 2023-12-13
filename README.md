# KinBP
KinBP is a drop-in replacement controller for [Kinesis Contoured keyboards](https://deskthority.net/wiki/Kinesis_Contoured).

It serves the same purpose as [KinT controller](https://github.com/kinx-project/kint) created by Michael Stapelberg.

![KinBP v1.2](https://i.imgur.com/tfWhnpxh.jpg)

## Features and advantages
- Controller with [QMK firmware](https://qmk.fm/) support.
- Uses inexpensive [WeAct Studio STM32F401/STM32F411](https://github.com/WeActTC/MiniSTM32F4x1) MCU board. The cost of manufacturing 5 sets is about 12 USD per controller. The PCB has dimensions less than 100×100 mm. Many manufacturers provide additional discounts for smaller boards.
- Compatible with all Kinesis Contoured keyboards but the earliest models (100/110/120).
- Additional pads for connecting up to 8 swithes (i.e. additional switches on the keyboard or foot pedals).
- Replacement thumb cluster PCBs with reversible design. They may be needed for some of 13x models (see below). 
- Thumb cluster switch mounting plates.

## Changelog
1.21
- added 7-pin 1.25mm connector footprints (micro JST) for custom thumb cluster PCBs
- added spare footprints upside down for connectors with pins on the other sideю

## BOM
###  Connectors
The choice of connectors depends on the keyboard model:
 - KB600 (Advantage2).
 1. 6x 13-pin FPC connectors. [Molex 39-53-2135](https://octopart.com/39-53-2135-molex-7670149?r=sp).  Please note that the cheap (5 USD for 20 pcs) [connectors from Aliexpress](https://aliexpress.com/item/1005001616368875.html?item_id=1005001616368875&sku_id=12000016826250362&spm=a2g2w.productlist.0.0.388b79adVkSP7k) are polarised and can only be used for the top row connectors on the KB600; using them in the other positions will not work because the pads on the FPC cable are on the wrong side and the cables are too short to be twisted.

 - KB500 (Advantage).
 1. Connecting keywells and top rows: 4x 13-pin FPC connectors, same as mentioned above.
 2. Connecting thumb cluster PCBs: 2x 10-pin angled 2.54mm headers.

 - KB13x (Essential, Classic, Professional).
 1. Connecting keywell PCBs: 2x [angled 13-pin FPC connectors](https://aliexpress.com/item/32896882494.html?gatewayAdapt=glo2rus&item_id=32896882494&sku_id=65719775344&spm=a2g0s.12269583.0.0.716190456RjJJP).
 2. Connecting top rows: same angled connectors or straight (same as for KB500/KB600).
 3. Some models had LEDs on the thumb cluster PCBs instead of the controller PCB. In this case you will need a pair of new thum cluster PCBs, optional switch mounting plates (see below) and set of cables/connectors with 1.25mm pitch: 2x [7 pin micro JST 10cm cables](https://aliexpress.com/item/4000588750065.html?sku_id=10000003451067244&spm=a2g0o.store_pc_allProduct.8148356.2.6c274451oTiXZp&gatewayAdapt=glo2rus) + 4x [7 pin micro JST angled connector](https://aliexpress.com/item/4000587245338.html?spm=a2g0o.store_pc_allProduct.8148356.8.3bf42024ng7J27&pdp_npi=2%40dis%21RUB%2184%2C24%20%D1%80%D1%83%D0%B1.%2184%2C24%20%D1%80%D1%83%D0%B1.%21%21%21%21%21%40211675ce16784397398875718e4cd2%2110000003439523920%21sh&sku_id=10000003439523925).
 
 Example of incompatible stock thumb cluster PCBc (Kinesis Professional KB134PC): ![KB134PC controller](https://i.imgur.com/KSjBS69h.jpg)
 
 You can also reuse connectors from an stock controller, but desoldering them can be tricky. Please note that the Chinese aliexpress connectors and some of the older connectors only had contacts on one side. For the top rows, you need to position the connector so that the contacts are on the outside (there are two footprints for this): ![top row connector](https://i.imgur.com/WiBvV45h.jpg)
 
### Controller PCB (/controller-pcb).
  - [WeAct Studio STM32F401 or STM32F411](https://github.com/WeActTC/MiniSTM32F4x1) board. You can buy them for about 6 USD at the [official Aliexpress store](https://weactstudio.aliexpress.com/). Beware of pirated copies!
  ![KinBP v1.21](https://i.imgur.com/enW1L5uh.png)
  - 4 pcs 3-mm LEDs
  - 4 pcs 0805 or through-hole resistors. Their value depends on the type of LEDs (I use 1.5k Ohm for orange LEDs).
  - Pair of USB Type C male and female connectors.
###  Thumb cluster (/thumb-pcb)
  - The design is reversible. So, a minimal batch of 5 PCBs will give you 2 pairs + 1 spare.
  ![Thumb PCB](https://i.imgur.com/cEafu8ph.png)
  ![Thumb PCB](https://i.imgur.com/XnGld7Fh.png)
  - 12x SOD-123 1N4148 diodes.
  - Optional [switch mounting plates](https://github.com/DmNosachev/kin80/tree/main/plates/thumb)
  - set of connectors and cables (see above)
### Switches
  - Optional: 68 pcs Cherry MX compatible switches.
  
## Buid guide
1. Test your keyboard. Identify faulty switches. Decide if you like the switches (most of the time there will Cherry Browns) and the top row rubber buttons. If rubber buttons are unacceptable to you and you do not mind spending a lot of time on hand-wiring, then it is worth considering an alternative project — (Kin80)[https://github.com/DmNosachev/kin80].
2. Disassemble the keyboard. Remove all screws and remove all PCBs. If some of the rubber buttons don't work well, the top row assembly can be taken apart and repaired by sticking pieces of copper tape on the button bottoms. Use hot-melt adhesive to asseble it back.
3. Assemble the controller PCB.
4. Optional: assemble thumb cluster PCBs.
5. Case. Seal the holes on the back of the case with pieces of plastic. Glue the USB connector to the back of the case. Optional: use bitumen sound deadening pads to improve acoustics.
6. [Setup the QMK](https://docs.qmk.fm/).
7. Flash the firmware: `qmk flash -kb kinbp -km default`. Hold 'boot0' button on MCU board, press 'reset', then release 'boot0' to enter bootloader.

## TODO
- FR4 mounting plate for the thumb cluster.
- Create universal or separate PCB with RP2040 support.
