# Altium Libraries for JLCPCB Parts

This repository contains automatically generated schematic libraries for a range of parts in JLCPCB's catalogue. In total this repository contains over 55000 parts.

![preview](preview.png)

Component information is pulled from JLCPCB's website, LCSC's metadata, and [yaqwsx's parametric search](https://yaqwsx.github.io/jlcparts/), is parsed into an intermediate JSON format, and a SchLib file is directly generated using my unreleased .NET library for Altium documents.

The current library files are:

 - `jlcpcb_resistors_basic.schlib` - All 0402, 0603, and 0805 package resistors in the JLCPCB basic parts catalogue (approximately 256 parts)
 - `jlcpcb_capacitors_basic.schlib` - All 0402, 0603, and 0805 package capacitors in the JLCPCB basic parts catalogue (approximately 109 parts)
 - `jlcpcb_resistors_extended.7z` - Archive containing schematic library files (organised by package size) for chip resistors in package sizes 01005, 0201, 0402, 0603, 0805, 1008, 1206, 1210, 1806, 1812, 2010, 2512, and 2910 from the in-stock JLCPCB extended parts catalogue (approximately 44387 parts total)
 - `jlcpcb_capacitors_extended.7z` - Archive containing schematic library files (organised by package size) for MLCC capacitors in package sizes 01005, 0201, 0402, 0603, 0805, 1008, 1206, 1210, 1806, 1812, 2010, 2512, and 2910 from the in-stock JLCPCB extended parts catalogue (approximately 10723 parts total)

Extended parts libraries are split up into separate SchLib files per package size because a combined SchLib file is too large and takes more than an hour to open.

## Warning

These schematic library files are **automatically generated**. The accuracy of the data is limited to the accuracy of the JLCPCB and LCSC parametric data. Always double check parametric data with the datasheet before assuming that a part is suitable for your needs.

## Parametric Information

Each part has parametric information filled out, based on the API data from JLCPCB and LCSC.

### Common Parameters

All parts have the following parameters set:

- Manufacturer
- Manufacturer Part Number
- JLCPCB Part Number
- JLCPCB Basic Part ("Yes" or "No")
- Package Size
- Category
- Datasheet link
- JLCPCB Part URL link

Each component references a footprint named with the format `TYPE-SIZE`, e.g. `RES-0603` or `CAP-0805`, in any loaded library. All you need is a PcbLib with those three footprints (you can create them with the IPC Footprint Wizard if you don't already have suitable ones) and they'll automatically be picked up from there within your project.

### Resistors

Each resistor has the following parameters populated if they are present in the JLCPCB/LCSC parametric data, in addition to the common parameters:

- Resistance
- Tolerance
- Power Rating
- Voltage Rating
- Temperature Rating
- Temperature Coefficient

### Capacitors

Each capacitor has the following parameters populated if they are present in the JLCPCB/LCSC parametric data:

- Capacitance
- Tolerance
- Voltage Rating
- Temperature Coefficient
- Temperature Rating

## License

All schematic library files in this repository are released into the public domain.

## Support / Donations

I have had a few people ask if I take donations for this work. I don't have anything set up right now, but if you want to support this project you can take a look at my parody warning stickers over at [Unsafe Warnings](https://www.etsy.com/shop/UnsafeWarnings/).

The creation of these libraries wouldn't be possible without [yaqwsx's JLCPCB parametric search project](https://yaqwsx.github.io/jlcparts/), so please check it out and consider sending him a few buckaroos via his Ko-Fi link.
