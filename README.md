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

The design item ID for each part is set to the manufacturer's part number, with any special characters replaced with underscores. When several components in the same library have the same name, the LCSC product ID (e.g. C1234) is added as a suffix.

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

## Footprints

Each component references a footprint named with the format `TYPE-SIZE`, e.g. `RES-0603` or `CAP-0805`. These footprint references are configured to be sourced from any library, so you can create an appropriate footprint with the correct name in any PcbLib in your project and Altium will automatically pick it up and use it for every single part of that type and size.

Footprints are **not included** in this repository - this is a conscious choice. Even though the component package sizes are standardised, each PCB designer has their own specific preferences and requirements in terms of exact footprint specifications.

Here are some of the issues and variables that would need to be contended with for providing "standardised" footprints:

- Solder fillet sizes and land protrusion varies based on the chosen IPC-7351 density class.
- Some designers prefer or mandate the use of keepout regions under packages:
  - The size and shape of the keepout region is specific to the rules set by the designer.
  - The types of objects that are disallowed (e.g. traces, pours, vias, etc.) may vary.
  - The rules for keepout regions may be different for different component sizes. For example, you might choose to disallow traces under packages smaller than 1206, but allow them for larger packages.
  - The rules for keepout regions may be different for different component types. For example, you might be OK with having vias inside the 
- There is no standard height range for SMD chip components, and no package height information is included with the JLCPCB/LCSC parametric data, so the footprint height metadata and generated STEP model may not accurately reflect the true height of the package.
- Altium's [IPC Compliant Footprint Wizard](https://www.altium.com/documentation/altium-designer/footprintwizard-dlg-form-footprintwizardipc-compliant-footprint-wizard-ad) does not necessarily always produce ideal footprints:
  - In some cases it may tend towards creating slightly oversized pads. I have personally run into cases where JLCPCB's engineers have had to manually reduce the footprint size for manufacturability.
  - In some cases the default paste mask expansion may not be ideal for JLCPCB's assembly process.

Providing standardised footprints in this repository would likely lead to a situation where most people just used them without thinking about correctness or suitability. If I made a mistake on a footprint, this could lead to all sorts of annoyances and problems for PCB designers and JLCPCB's assembly technicians.

### Creating Footprints

Creating the footprints yourself is not as much of a chore as you might initially think. Altium's [IPC Compliant Footprint Wizard](https://www.altium.com/documentation/altium-designer/footprintwizard-dlg-form-footprintwizardipc-compliant-footprint-wizard-ad) will automatically generate a footprint for you (complete with STEP model) based on a specified set of dimensions, and you can find the correct dimensions for each SMD passive package size online.

I would recommend starting with the most common part sizes. For example, creating just the `RES-0402`, `RES-0603`, `RES-0805`, `CAP-0402`, `CAP-0603`, and `CAP-0805` footprints covers the entire basic library and 70% of the extended libraries (>38000 components) at time of writing. You can later create footprints for other component sizes, as and when you need them.

Ten minutes spent creating these footprints saves you roughly 1000 hours of data entry, had you created all of these parts libraries by hand, so it's not a bad trade-off ;)

## Updates

I cannot offer any guarantees regarding the frequency of ongoing updates to this library.

Since the auto-generated libraries are limited to in-stock parts only, updated releases of this library may remove parts that have been out of stock for more than 30 days.

The design item ID naming scheme should stay constant between updates, but the consistency is subject to changes in the input metadata and stocking status.

Out of an abundance of caution, I have taken care to ensure that consistent predictable UIDs are used for all internal structures within the generated SchLib files, rather than just randomly generating them. This shouldn't matter, but it helps reduce the potential for hitting bugs and edge-cases within Altium when you update the schematic library file.

## License

All schematic library files in this repository are released into the public domain.

I provide no warranty as to the validity, accuracy, or correctness of the parts within these libraries. Use them at your own risk.

## Support / Donations

I have had a few people ask if I take donations for this work. I don't have anything set up right now, but if you want to support this project you can take a look at my parody warning stickers over at [Unsafe Warnings](https://www.etsy.com/shop/UnsafeWarnings/).

The creation of these libraries wouldn't be possible without [yaqwsx's JLCPCB parametric search project](https://yaqwsx.github.io/jlcparts/), so please check it out and consider sending him a few buckaroos via his Ko-Fi link.
