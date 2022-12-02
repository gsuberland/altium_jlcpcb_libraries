# Altium Libraries for JLCPCB Parts

This repository contains automatically generated libraries for a range of parts in JLCPCB's catalogue.

![preview](preview.png)

Component information is pulled from JLCPCB's website, parsed into an intermediate JSON format, and a SchLib file is directly generated using my unreleased .NET library for Altium documents.

I have initially generated a SchLib file that contains entries for all 0402, 0603, and 0805 resistors in the JLCPCB Basic Parts catalogue. Each resistor has the following parameters populated:

- Manufacturer
- Manufacturer Part Number
- LCSC Part Number
- Package Size
- Resistance
- Resistance Tolerance
- Power Rating
- Voltage Rating
- Temperature Rating
- Temperature Coefficient
- Datasheet link
- JLCPCB Part URL link

Each component also has a "JLCPCB Basic Part" property with a value of "Yes", and the category property is filled out.

Each component references a footprint named RES-0402, RES-0603, or RES-0805 in any loaded library. All you need is a PcbLib with those three footprints (you can create them with the IPC Footprint Wizard if you don't already have suitable ones) and they'll automatically be picked up from there within your project.

