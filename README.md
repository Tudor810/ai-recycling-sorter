# AI Recycling Sorter

An embedded system that identifies a waste item and routes it to the correct bin following Romanian recycling rules, including the SGR deposit-return system (*Sistemul Garanție-Returnare*).

Course project for **PMP** (UTCN, year 3).

## How it works

1. **Detect** – an item is dropped into the inspection chamber; the load cell registers it.
2. **Classify** – the camera image is classified by an AI model, then combined with the sensor readings (weight, inductive metal sensor) using deterministic rules.
3. **Set gate** – the ESP32 swings the servo diverter gate for the target bin across the conveyor.
4. **Convey** – the trapdoor opens, the item drops onto the belt and is carried to its gate; break-beam sensors confirm its position.
5. **Divert** – the gate guides the item off the belt into its bin. Items that match no gate ride off the end into residual.
6. **Update** – ultrasonic sensors measure fill levels; the app updates counts, statistics and the SGR deposit total.

## Bins

| Bin | Contents |
|---|---|
| Yellow | Plastic and metal |
| Blue | Paper and cardboard |
| SGR returns | Drink containers with the "Ambalaj cu garanție" logo (0.50 lei deposit each) |
| Residual | Everything else, including low-confidence items |

## Hardware

- **Controller:** ESP32-S3
- **Sensors:** camera, load cell + HX711, inductive proximity sensor, IR break-beam sensors (one per gate + end of belt), ultrasonic fill sensors (one per bin), bin presence switches
- **Actuators:** DC gear motor + driver for the conveyor, servo for the trapdoor, one servo per diverter gate, status LEDs and buzzer

## Repository layout

| Folder | Contents |
|---|---|
| `firmware/` | ESP32 firmware: sensors, motor and servo control, communication |
| `ai/` | Dataset notes, model training and the inference server running on the laptop |
| `app/` | Phone / web dashboard: fill levels, statistics, labeling of uncertain items |
| `hardware/` | Wiring diagrams, bill of materials, CAD / 3D models |
| `docs/` | Project documentation and report |

## Status

Early setup – structure only.
