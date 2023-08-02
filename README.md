# Dremel-PCB1857V1

Reverse engineering of a Dremel 12v battery charger.
The pcb has the markings: PCB1857V1
This repository contains KiCad schematics of the main side of its power supply.
Component values have been measured and added.

## Attention

Pads lift very easily on this old pcb.

## Troubleshooting

### Evidence

- C2 blown
- R10 blown
- F1 blown
- V5 blown

### 1. Attempt

Replaced parts:  
- F1 
- V5 with P7NK80Z
- R10 with (see notes)
- C2 with 33 uF 450 V electrolytic

Result:  
- F1 blown
- R10 blown again
- C2 blasted from the outside by R10
- V5 maybe damaged
- V6 damaged
- R6 measures 3.3k instead of 30 R (nominal)

### 2. Attempt

Replaced parts:
- R30 (10k) with 11k (out of 10k)
- V11 (IN4007)
