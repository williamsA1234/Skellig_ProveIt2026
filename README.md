# Skellig ProveIt 2026 — SM Profiles

CESMII Smart Manufacturing Profile definitions for single-use bioprocessing equipment, published as part of [ProveIt! 2026](https://www.proveitconference.com/).

These profiles describe the data contracts for equipment types used in our Unified Namespace. They are derived from **Inductive Automation Ignition UDT definitions** and published here so that any consumer can understand the structure of our data without needing access to our Ignition gateway or message broker.

## What Is An SM Profile?

An SM Profile is a type definition — a contract that says "data of this type will have these attributes, these data types, these parameters."

- **For a publisher**, it's a promise that the data will look a certain way.
- **For a consumer**, it means their logic/app/analysis can work anywhere that promise is kept.

For more background, see [CESMII ProveIt-SMProfiles](https://github.com/cesmii/ProveIt-SMProfiles).

## Profiles

### Core Building-Block Profiles

These are reusable base profiles corresponding to the `Core/` UDT folder in Ignition. Equipment-specific profiles (below) are built from combinations of these I/O patterns.

| Profile | I/O | Description | Ignition UDT |
|---------|-----|-------------|--------------|
| [DeviceCore_V1](DeviceCore_V1.json) | — | Equipment identity and context metadata (TagName, Area, Unit, etc.) | `Core/DeviceCore` |
| [Unit_V1](Unit_V1.json) | — | ISA-88 unit with batch context (State, BatchID, Formula, etc.) | `Core/Unit` |
| [AI_V1](AI_V1.json) | AI | Analog input with four-level limit alarms | `Core/AI` |
| [AI_AO_V1](AI_AO_V1.json) | AI + AO | Analog input + analog output | `Core/AI_AO` |
| [AI_AO_DI_V1](AI_AO_DI_V1.json) | AI + AO + DI | Analog input/output + digital input | `Core/AI_AO_DI` |
| [AI_AO_DI_DO_V1](AI_AO_DI_DO_V1.json) | AI + AO + DI + DO | Full analog + digital I/O | `Core/AI_AO_DI_DO` |
| [AI_AO_DI_DO_M_V1](AI_AO_DI_DO_M_V1.json) | AI + AO + DI + DO | Full I/O with Mode parameter | `Core/AI_AO_DI_DO_M` |
| [AI_AO_DI_M_V1](AI_AO_DI_M_V1.json) | AI + AO + DI | Analog input/output + digital input with Mode | `Core/AI_AO_DI_M` |
| [AI_AO_DO_M_V1](AI_AO_DO_M_V1.json) | AI + AO + DO | Analog input/output + digital output with Mode | `Core/AI_AO_DO_M` |
| [DI_V1](DI_V1.json) | DI | Digital input with bad quality detection | `Core/DI` |
| [DO_V1](DO_V1.json) | DO | Digital output with bad quality detection | `Core/DO` |

### Equipment-Specific Profiles

These profiles are derived from the core building blocks and map to the `ProveIt/` UDT folder in Ignition, with equipment-specific IO tag names (e.g., `Speed_PV`, `Flow_SP`, `Valve_Position_PV`).

| Profile | I/O | Description | Ignition UDT |
|---------|-----|-------------|--------------|
| [Agitator_AI_AO_V1](Agitator_AI_AO_V1.json) | AI + AO | Agitator with speed PV and speed SP | `ProveIt/Agitator_AI_AO` |
| [Agitator_AI_AO_DO_M_V1](Agitator_AI_AO_DO_M_V1.json) | AI + AO + DO | Agitator with speed control, start command, and Mode | `ProveIt/Agitator_AI_AO_DO_M` |
| [AIC_AI_AO_DI_V1](AIC_AI_AO_DI_V1.json) | AI + AO + DI | Analytical controller (pH, DO, conductivity) with control active | `ProveIt/AIC_AI_AO_DI` |
| [FCV_AI_V1](FCV_AI_V1.json) | AI | Flow control valve with position feedback only | `ProveIt/FCV_AI` |
| [FCV_AI_AO_V1](FCV_AI_AO_V1.json) | AI + AO | Flow control valve with position PV and SP | `ProveIt/FCV_AI_AO` |
| [FIC_AI_AO_V1](FIC_AI_AO_V1.json) | AI + AO | Flow indicating controller with flow PV and SP | `ProveIt/FIC_AI_AO` |
| [FIC_AI_AO_DI_V1](FIC_AI_AO_DI_V1.json) | AI + AO + DI | Flow controller with control active and Bypass | `ProveIt/FIC_AI_AO_DI` |
| [PIC_AI_AO_V1](PIC_AI_AO_V1.json) | AI + AO | Pressure indicating controller with pressure PV and SP | `ProveIt/PIC_AI_AO` |
| [Pump_AI_V1](Pump_AI_V1.json) | AI | Pump with speed feedback only (monitor) | `ProveIt/Pump_AI` |
| [Pump_AI_AO_V1](Pump_AI_AO_V1.json) | AI + AO | Pump with speed PV and speed SP | `ProveIt/Pump_AI_AO` |
| [Pump_AI_AO_DI_M_V1](Pump_AI_AO_DI_M_V1.json) | AI + AO + DI | Pump with start confirmation and Mode | `ProveIt/Pump_AI_AO_DI_M` |
| [Pump_AI_AO_DI_DO_V1](Pump_AI_AO_DI_DO_V1.json) | AI + AO + DI + DO | Pump with full I/O (start confirm + run command) | `ProveIt/Pump_AI_AO_DI_DO` |
| [Pump_AI_AO_DI_DO_M_V1](Pump_AI_AO_DI_DO_M_V1.json) | AI + AO + DI + DO | Pump with full I/O and Mode | `ProveIt/Pump_AI_AO_DI_DO_M` |
| [Temp_AI_AO_DI_M_V1](Temp_AI_AO_DI_M_V1.json) | AI + AO + DI | Temperature controller with status and Mode | `ProveIt/Temp_AI_AO_DI_M` |
| [TIC_AI_AO_V1](TIC_AI_AO_V1.json) | AI + AO | Temperature indicating controller with temp PV and SP | `ProveIt/TIC_AI_AO` |
| [Valve_DO_V1](Valve_DO_V1.json) | DO | On/off valve with digital output command | `ProveIt/Valve_DO` |

## A Note On `opc:` Data Types

You'll see data types like `opc:String`, `opc:Boolean`, `opc:Double` throughout these profiles. **This does NOT mean the data must come from OPC UA or that you need OPC UA to use it.** 

`opc:` is just a namespace prefix referencing the [OPC UA data type definitions](https://reference.opcfoundation.org/v105/Core/docs/Part6/) as a universal vocabulary. It's the same reason CESMII chose OPC UA Information Models as their starting point — they're a well-defined, platform-neutral set of type definitions that everyone can agree on. `opc:String` simply means "this is a string." `opc:Boolean` means "this is true/false." 

These profiles are protocol-agnostic. You could implement them using **MQTT**, **OPC UA**, or any other messaging protocol. The `opc:` prefix is just a common language for describing data types so that any platform — Ignition, FactoryTalk, Node-RED, Python, whatever — can read these profiles and understand what to expect.

## Profile Structure

Each `.json` file defines four sections:

### Device_Core
Equipment identity and context metadata — ISA-5.1 tag name, ISA-95 area/unit, human-readable short name, equipment type, and a `ProfileDefinition` URL linking back to this repo.

### IO
Live process I/O that could be bound to field instruments via MQTT, OPC UA, or other protocols. Engineering units are **per-instance** where applicable — the profile declares that an eng unit property exists, but the actual unit (RPM, percent, LPM, etc.) is set when the instance is created.

### Parameters
Configurable values for alarm thresholds, output limits, and operating modes. Set per-instance, typically do not change during normal operation.

### Alarms
Reference tags for Ignition alarm evaluation. Each alarm tag's value mirrors an IO process variable that an Ignition alarm property evaluates against. For analog types, this includes four-level limit alarms (High_High, High, Low, Low_Low) and bad quality detection. Digital types include bad quality detection. Most profiles also include an ESTOP memory tag. **Alarm active/inactive state is not published in this profile version** — the alarms are configured as Ignition alarm properties on these reference tags and are evaluated locally within Ignition.

## Implementation

These profiles can be implemented using various platforms and protocols:

- **Platform**: Could be Inductive Automation Ignition, FactoryTalk, Node-RED, or any other platform
- **IO Source**: Could use MQTT, OPC UA, or other messaging protocols
- **Alarms**: Configured as platform-native alarm properties on reference tags (alarm active/inactive state is not published in this version)
- **Parameters**: Configurable per instance, typically stored as tags or variables
- **UNS**: Data could be published to MQTT broker, OPC UA server, or other Unified Namespace implementations

Each instance should carry a `Device_Core.ProfileDefinition` tag or property linking to the corresponding `.json` file in this repo.

## File Naming Convention

| File | Purpose |
|------|---------|
| `TypeName_V1.json` | The SM Profile definition (the contract) |
| `coreexport.json` | Ignition UDT export for the `Core/` folder (base building-block types) |
| `proveitexport.json` | Ignition UDT export for the `ProveIt/` folder (equipment-specific types) |

## References

- [CESMII SM Profiles](https://www.cesmii.org/technology/sm-profiles/)
- [CESMII ProveIt-SMProfiles](https://github.com/cesmii/ProveIt-SMProfiles)
- [OPC UA Information Model (Part 5)](https://reference.opcfoundation.org/v105/Core/docs/Part5/)
- [ISA-18.2 Alarm Management](https://www.isa.org/standards-and-publications/isa-standards/isa-standards-committees/isa18)

## License

CC0-1.0
