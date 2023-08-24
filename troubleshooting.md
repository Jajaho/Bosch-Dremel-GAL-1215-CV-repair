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
- R5 (?R) with 2.5W 0.47R 

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
- Resolve R15/R5 naming conflict in schematic
- try higher value for R5


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

### 3. Attempt

#### Replaced parts
- V5 replaced with STP7NK80Z


#### 1. Powerup
   
   230V ac at line input
   results in no current draw
    325VDC across C2
   Vdd and Vcc measure 0V (measured across cap respectively)
   L3 and L4 both 5V ac across

### 22.08.23
mit Harry 
   - V1 measures +350mV Vce but 0V Vbe - tested: defect
   - replaced V1 
      But how could V1 have gotten destroyed?

   - V5 in circuit the we measured 2.25V at the gate (relative to gnd)
   - v5 has been removed and ttester checked out
   -R11, R15 checked out
   - R4 itself measured ok (47kOhm)
   But with it desoldered we measured 7.5 kOhm across it's terminals 
   Next step: Find out through what path this resistance comes from
               - desolder V1
               - Check C5 and C16

### 23.08.23 

- desoldered C16 10kOhm still across R4 footprint (with R4 removed)
- desoldered V1, ttester result: 1 - 1.31 Ohm - 2 - 120 Ohm - 3
- Now there is no connection across R4 footprint
- Reinstalled all previously desoldered resistors and caps (expcept V1 and V5)
   - Powered up: V1: Vbe = 0 V, Vce = 13.75 V, V2: Vgs = 13.77 V
- Desoldered U1 (optocoupler) and tested it with a psu - ok.
- Reinstalled U1 and V1, power up, Vbe = 13.80 V
- Reinstalled V5
- Changed R5 from 0.15 Ohm to 2 Ohm (2 x 3.9 Ohm MF0207 in parallel)
- Power up: - Resonant circuit is working! f = 4880 kHz
            - Secondary side terminals have only Vrms = 1.9 V and Vrms = 1.2 V 
            - Secondary side electrolytics measure ~ 400 mV DC
            - Green led is lighting up

Channel legend on prints:
CH2 - V1, Vce
CH3 - V1, Vbe
CH4 - V5, Vds

What killed the npn? - We will never know

- Too much Ic? - Theoretically there could flow a maximum current of 0.5A through V1 because the voltage divider. But R11/R15 limit that so that at the maximum rated current of Ice of 200mA (continuous) there would need to bee a voltage drop of 200 kV across R11 and R15.
- Vbe bigger then 6 V?

Resonanzfrequenz

f = 1/(2*pi*sqrt(L*C))

with L = 9.31 uH / C = 10 nF gives f = 5216 kHz which is close to the measured 4880 kHz switching frequency -> C5/TR1_L1 must be the main resonant circuit