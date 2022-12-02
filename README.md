# Altium Libraries for JLCPCB Parts

This repository contains automatically generated libraries for a range of parts in JLCPCB's catalogue.

![preview](preview.png)

Component information is pulled from JLCPCB's website, parsed into an intermediate JSON format, and a SchLib file is directly generated using my unreleased .NET library for Altium documents.

I have generated a SchLib files that contain entries for all 0402, 0603, and 0805 resistors and capacitors in the JLCPCB Basic Parts catalogue. At time of writing, this totals 365 parts. This saves a lot of the manual usually required to create the parts.

## Common Parameters

All parts have the following parameters set:

- Manufacturer
- Manufacturer Part Number
- JLCPCB Part Number
- JLCPCB Basic Part ("Yes" or "No")
- Package Size
- Category
- Datasheet link
- JLCPCB Part URL link

Each component references a footprint named with the format `TYPE-SIZE`, e.g. `RES-0603` or `CAP-0805`, in any loaded library. All you need is a PcbLib with those three footprints (you can create them with the IPC Footprint Wizard if you don't already have suitable ones) and they'll automatically be picked up from there within your project. Only 0402, 0603, and 0805 parts exist in these SchLib files, so you only need to create six footprints in total to match the hundreds of parts in these libraries.

## Resistors

Each resistor has the following parameters populated, in addition to the common parameters:

- Resistance
- Tolerance
- Power Rating
- Voltage Rating
- Temperature Rating
- Temperature Coefficient

## Capacitors

Each capacitor has the following parameters populated:

- Capacitance
- Tolerance
- Voltage Rating
- Temperature Coefficient