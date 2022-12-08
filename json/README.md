# Parts as JSON

This is a **work in progress**.

These are JSON files that describe parts in the JLCPCB basic parts catalogue in a generic way.

These are not the same as the intermediate JSON format used by the current library generator code, which is instead focused on parametric information that is applied to a generic symbol and footprint.

These JSON files are part of an ongoing project to auto-generate both symbols and footprints for all JLCPCB parts in Altium. The JSON format should be usable for library generation for any EDA tool, which is why I'm publishing them here.

Currently, each JSON file contains various information about the part along with symbol and footprint features. The features can be used to recreate the part's symbol and footprint in an EDA library.

Each part has a `symbols` array property. If the part has multiple subparts (e.g. a hex inverter chip with 6 separate inverters) each subpart will be included as a symbol. Each symbol has a `canvas_properties` object that describes the coordinate system and the way the editor was set up while the symbol was created, and a `features` array that describes each of the features in the symbol. The exact properties of each feature depends on its type, which can be found in the `type` property. Most of it is self-explanatory.

Each part has a `footprint` array property. Each object inside describes a footprint feature, e.g. a pad, track, or solid region. Again, the properties are largely self-explanatory.

