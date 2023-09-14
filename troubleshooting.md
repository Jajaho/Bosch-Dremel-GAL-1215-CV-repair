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

![](prints/V5%20measurement%201%20V5%2023-08-23/DS1Z_QuickPrint1.png)
(All measurements are with respect to gnd)

legend:  
CH2 - V1, Vce  
CH3 - V1, Vbe  
CH4 - V5, Vds  

![](prints/V5%20measurement%203%2023-08-23/DS1Z_QuickPrint2.png)

legend:  
CH1 - Voltage at the cathode of *D6  (because it defines the working point of V1)  
CH2 - V5 Vds  
CH3 - V5 Vgs  
CH4 - V1 Vbe 

The voltage across R19 (above optocoupler U1) was also measured during operation. 
The secondary side can't influence the primary side however because the op-amps are not powered.

Conclusions: 
The working point of V1 should be about 4.583 V according to the voltage divider.
But a measurement shows that Vbe of V1 never exceeds 1 V (ignoring oscillations)

#### What killed the npn? - We will never know

- Too much Ic? - Theoretically there could flow a maximum current of 0.5A through V1 because the voltage divider. But R11/R15 limit that so that at the maximum rated current of Ice of 200mA (continuous) there would need to bee a voltage drop of 200 kV across R11 and R15.
- Vbe bigger then 6 V?

Resonant frequency

f = 1/(2*pi*sqrt(L*C))

with L = 9.31 uH / C = 10 nF gives f = 5216 kHz which is close to the measured 4880 kHz switching frequency -> C5/TR1_L1 must be the main resonant circuit

### 24.08.23

- Added two parallel 4.3 Ohm resistors in parallel to the already installed 1.95 Ohm for a total of 4.1 Ohms for the blown R5.
   - subsequent power up: The voltage on the secondary side decreased further to ~ 0.75 Vrms. 
- Replaced R5 with 1 Ohm resistor.
   - subsequent power up: secondary side Vrms = ~ 1.2 Vrms

   ![](prints/V5%20measurement%204%2024-08-23/DS1Z_QuickPrint3.png)

   Observations:   
   - Significantly less ringing  
   - V5 switches off once Vbe of V1 reaches 0.890 V which now takes 1.48 us

- Replaced R5 with 0.6 Ohm resistor.
   - subsequent power up: Less then a second operation, death
   - Desoldered V1, ttested: diode from 1 to 3 and from 2 to 3, failed.

- Replaced R5 with 0.8 Ohm, replaced V1
   - subsequent power up: Less then a second operation, death
   - tested V1 in circuit, 7.5 kOhm between C/E (like previously), 17 ohm between b/e

- Replaced Fuse (wasn't blown but looked burned)
- Replaced V1 and R5 with 1 Ohm again
   - subsequent power up: 1.15 Vrms at the secondary, but briefly up to 7 Vrms, might be something during the power up.
   - Further measurements of the secondary side cap show that even though the uni-t UT61D showed ~ 100 mV DC the oscilloscope showed Vavg = 1.64 V and significant ripple

- Plugged in a battery (while powered on): Bang, sparks, firework, death.  
   - Damaged parts: F1 and R5 blew violently, C2 caught in R5s blast, R6 visibly damaged. V5 not visibly damaged
   - R5 now measures 62 kOhm
   - F1 is open line
   - R6 now measures 10.5 kOhm
   - V1 Rbe = 2.7 Ohm, Rce = 25.7 Ohm
   - V5 Rgs = 22 ohm, Rds = 11.3 Ohm
   - Pad of V5 gate lifted!!!

   - Theory: The supply voltage is kept low to safe power while the battery charger is idling. Once a battery is detected by the micro controller it increases the secondary side voltage to match the desired charging current (cc charging phase) or if the voltage is already big enough cv. This is achieved via the optocoupler U1. By increasing the photo-transistors c/e-resistance the Vbe of V1 is decreased which again increases Vgs of V5, letting current flow for a longer portion of a period.

### 14.09.23

Bosch pcb tested:
- Idle 
   - mains current ~ 0 mA
   - V_C2 = 320 VDC
   - VDD zu GND1 (across the larger secondary side cap) = 1.550 VDC
   - VCC to GND2 (across the 220 uF cap) = 13.07V
   - AKKU+ to AKKU- V = 1.5 VDC

   