# Skellig ProveIt 2026 — SM Profiles

CESMII Smart Manufacturing Profile definitions for single-use bioprocessing equipment, published as part of [ProveIt! 2026](https://www.proveitconference.com/).

These profiles describe the data contracts for equipment types used in our Unified Namespace. They are derived from **Inductive Automation Ignition UDT definitions** and published here so that any consumer can understand the structure of our data without needing access to our Ignition gateway or MQTT broker.

## What Is An SM Profile?

An SM Profile is a type definition — a contract that says "data of this type will have these attributes, these data types, these alarms, these parameters."

- **For a publisher**, it's a promise that the data will look a certain way.
- **For a consumer**, it means their logic/app/analysis can work anywhere that promise is kept.

For more background, see [CESMII ProveIt-SMProfiles](https://github.com/cesmii/ProveIt-SMProfiles).

## Profiles

| Profile | I/O | Description | Ignition UDT |
|---------|-----|-------------|--------------|
| [Agitator_AI_AO_V1](smprofiles/Agitator_AI_AO_V1.jsonld) | AI + AO | Agitator with speed PV and speed SP | `ProveIt/Agitator_AI_AO` |
| [Agitator_AI_AO_DO_M_V1](smprofiles/Agitator_AI_AO_DO_M_V1.jsonld) | AI + AO + DO | Agitator with speed control, start command, and Mode | `ProveIt/Agitator_AI_AO_DO_M` |
| [AIC_AI_AO_DI_V1](smprofiles/AIC_AI_AO_DI_V1.jsonld) | AI + AO + DI | Analytical controller (pH, DO, conductivity) with control active | `ProveIt/AIC_AI_AO_DI` |
| [FCV_AI_V1](smprofiles/FCV_AI_V1.jsonld) | AI | Flow control valve with position feedback only | `ProveIt/FCV_AI` |
| [FCV_AI_AO_V1](smprofiles/FCV_AI_AO_V1.jsonld) | AI + AO | Flow control valve with position PV and SP | `ProveIt/FCV_AI_AO` |
| [FIC_AI_AO_V1](smprofiles/FIC_AI_AO_V1.jsonld) | AI + AO | Flow indicating controller with flow PV and SP | `ProveIt/FIC_AI_AO` |
| [FIC_AI_AO_DI_V1](smprofiles/FIC_AI_AO_DI_V1.jsonld) | AI + AO + DI | Flow controller with control active and Bypass | `ProveIt/FIC_AI_AO_DI` |
| [PIC_AI_AO_V1](smprofiles/PIC_AI_AO_V1.jsonld) | AI + AO | Pressure indicating controller with pressure PV and SP | `ProveIt/PIC_AI_AO` |
| [Pump_AI_V1](smprofiles/Pump_AI_V1.jsonld) | AI | Pump with speed feedback only (monitor) | `ProveIt/Pump_AI` |
| [Pump_AI_AO_V1](smprofiles/Pump_AI_AO_V1.jsonld) | AI + AO | Pump with speed PV and speed SP | `ProveIt/Pump_AI_AO` |
| [Pump_AI_AO_DI_M_V1](smprofiles/Pump_AI_AO_DI_M_V1.jsonld) | AI + AO + DI | Pump with start confirmation and Mode | `ProveIt/Pump_AI_AO_DI_M` |
| [Pump_AI_AO_DI_DO_V1](smprofiles/Pump_AI_AO_DI_DO_V1.jsonld) | AI + AO + DI + DO | Pump with full I/O (start confirm + run command) | `ProveIt/Pump_AI_AO_DI_DO` |
| [Pump_AI_AO_DI_DO_M_V1](smprofiles/Pump_AI_AO_DI_DO_M_V1.jsonld) | AI + AO + DI + DO | Pump with full I/O and Mode | `ProveIt/Pump_AI_AO_DI_DO_M` |
| [Temp_AI_AO_DI_M_V1](smprofiles/Temp_AI_AO_DI_M_V1.jsonld) | AI + AO + DI | Temperature controller with status and Mode | `ProveIt/Temp_AI_AO_DI_M` |
| [TIC_AI_AO_V1](smprofiles/TIC_AI_AO_V1.jsonld) | AI + AO | Temperature indicating controller with temp PV and SP | `ProveIt/TIC_AI_AO` |
| [Valve_DO_V1](smprofiles/Valve_DO_V1.jsonld) | DO | On/off valve with digital output command | `ProveIt/Valve_DO` |

## A Note On `opc:` Data Types

You'll see data types like `opc:String`, `opc:Boolean`, `opc:Double` throughout these profiles. **This does NOT mean the data comes from OPC UA or that you need OPC UA to use it.** 

`opc:` is just a namespace prefix referencing the [OPC UA data type definitions](https://reference.opcfoundation.org/v105/Core/docs/Part6/) as a universal vocabulary. It's the same reason CESMII chose OPC UA Information Models as their starting point — they're a well-defined, platform-neutral set of type definitions that everyone can agree on. `opc:String` simply means "this is a string." `opc:Boolean` means "this is true/false." 

Our actual data travels over **MQTT**, is stored in **Ignition tags**, and is bound to field instruments via **MQTT Engine**. No OPC UA protocol is involved. The `opc:` prefix is just a common language for describing data types so that any platform — Ignition, FactoryTalk, Node-RED, Python, whatever — can read these profiles and understand what to expect.

## Profile Structure

Each `.jsonld` file defines four sections:

### Device_Core
Equipment identity and context metadata — ISA-5.1 tag name, ISA-95 area/unit, human-readable short name, equipment type, and a `ProfileDefinition` URL linking back to this repo.

### IO
Live process I/O bound to field instruments via MQTT. Engineering units are **per-instance** where applicable — the profile declares that an eng unit property exists, but the actual unit (RPM, percent, LPM, etc.) is set when the instance is created.

### Parameters
Configurable values for alarm thresholds, output limits, and operating modes. Set per-instance, typically do not change during normal operation.

### Alarms
Alarm conditions following **ISA-18.2** patterns. Analog types use a four-level limit alarm model (High_High, High, Low, Low_Low). All types include bad quality detection and ESTOP.

## Implementation

- **Platform**: Inductive Automation Ignition
- **IO Source**: MQTT Engine (Cirrus Link) via MQTT broker
- **Alarms**: Ignition native alarm engine
- **Parameters**: Ignition memory tags, configurable per instance
- **UNS**: Data published to MQTT broker (Unified Namespace)

Each Ignition UDT instance carries a `Device_Core.ProfileDefinition` tag linking to the corresponding `.jsonld` file in this repo.

## File Naming Convention

| File | Purpose |
|------|---------|
| `TypeName_V1.jsonld` | The SM Profile definition (the contract) |
| `TypeName_V1.example.json` | Example payload showing real instance data |

## References

- [CESMII SM Profiles](https://www.cesmii.org/technology/sm-profiles/)
- [CESMII ProveIt-SMProfiles](https://github.com/cesmii/ProveIt-SMProfiles)
- [OPC UA Information Model (Part 5)](https://reference.opcfoundation.org/v105/Core/docs/Part5/)
- [JSON-LD Specification](https://www.w3.org/TR/json-ld11/)
- [ISA-18.2 Alarm Management](https://www.isa.org/standards-and-publications/isa-standards/isa-standards-committees/isa18)

## License

CC0-1.0
