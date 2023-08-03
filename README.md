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
- R5 (?R) with 2W 0.15 R 

Result:  
- F1 blown
- R10 blown again
- C2 blasted from the outside by R10
- V5 maybe damaged
- V6 damaged
- R6 measures 3.3k instead of 30 R (nominal)

### 2. Attempt

ToDo:
- V5 check

Replaced parts:
- F1 (1.25A)
- R30 (10k) with 11k (out of 10k)
- V11 (IN4007)
- V6 (2N 3904)
- R20 (2k)
- R14 (1k)
- C3 (100n) with smd 100n
- C2 (22uF) with 22uF 450V 
- R5 (?R) with 2W 0.15 R 

Power up 1:
Applying 10V AC to the line input causes about 1A of current.
R5 warms up extremely, confirmed by thermal camera.
Probable cause: 
- V5 overheated on previous attempt (print is discolored)
- R5 is to small
