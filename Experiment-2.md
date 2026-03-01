# Experiment 2

# DC, AC and Transient Analysis of MOSFET 
##  Aim
To design and simulate three MOSFET amplifier configurations using 180 nm CMOS technology in LTspice, perform DC, transient,
and AC analyses, and compare their gain, bandwidth, power consumption, and overall performance.
### CIRCUIT 1
### DC Analysis
This circuit is a Common Source (CS) amplifier with PMOS active load designed using 180 nm CMOS technology in LTspice.
<img width="611" height="542" alt="lab2ckt" src="https://github.com/user-attachments/assets/36bd7707-1d34-4c4c-9641-d3b50926e8b9" />
## PMOS Active Load

Instead of a passive resistor, a PMOS transistor is used as an active load.  
It provides high output resistance (ro), which increases gain.
For a CS amplifier:
Av ≈ − gm Rout  
Since Rout ≈ (ro_n || ro_p), higher ro gives higher gain.

## Source Degeneration

The source resistor RS introduces negative feedback.
Gain with source degeneration:
Av ≈ − gm (ro1 || ro2) / (1 + gm RS)

Effects:
- Improves linearity  
- Stabilizes bias point  
- Reduces gain  
Thus, PMOS active load increases gain, while source degeneration improves stability at the cost of reduced gain.

## Design Calculations 
### Given Specifications

- VDD = 1.2 V  
- ID = 200 µA  
- VOV = 0.25 V  
- CL = 0.5 pF  
- Ln = Lp = 180 nm
- P<= 0.4mW 
- εr = 3.9  
- ε0 = 8.854 × 10⁻¹² F/m  
- tox = 4.1 × 10⁻⁹ m  
- μn = 273.809 cm²/Vs  
- μp = 115.689 cm²/Vs  

### 1. Overdrive Voltage

For NMOS:

VOV = VGS − VTN  
Assume VTN = 0.36 V  

VGS = VOV + VTN  
VGS = 0.25 + 0.36  
VGS = 0.61 V  

### 2. Output Bias Point

Choose midpoint bias:

Vout ≈ VDD / 2 + 0.2  
Vout = 0.6 + 0.2  
Vout = 0.8 V  

### 3. Source Resistor (RS)

assume , VRS = 0.2 V  
ID = 200 µA  

RS = VRS / ID  
RS = 0.2 / (200 × 10⁻⁶)  
RS = 1 kΩ  

### 4. Oxide Capacitance (Cox)

Cox = εr ε0 / tox  
Cox = (3.9 × 8.854 × 10⁻¹²) / (4.1 × 10⁻⁹)  
Cox = 8.42 × 10⁻³ F/m²  

### 5. NMOS Width Calculation

Drain current equation:
ID = (1/2) μn Cox (W/L) (VOV)²  
Rearranging:
Wn = (2 ID L) / (μn Cox (VOV)²)
Substitute values:
Wn = (2 × 200 × 10⁻⁶ × 180 × 10⁻⁹)  
     / (273.809 × 10⁻⁴ × 8.42 × 10⁻³ × (0.25)²)
Wn ≈ 4.997 µm  

### 6. PMOS Width Calculation
Wp = (2 ID L) / (μp Cox (VOV)²)
Wp ≈ 11.823 µm  
By Varying Width
- Wp = 26.823 µm  → Id = 200 µA
- Wn = 30.195 µm  → Id = 200 µA

### 7. PMOS Gate Bias

For PMOS:
VOV = VSG − |VTP|  
Assume |VTP| = 0.39 V  

VSG = VOV + |VTP|  
VSG = 0.25 + 0.39  
VSG = 0.64 V  

Since:
VSG = VS − VG  
VS = VDD = 1.2 V  

VG = 1.2 − 0.64  
VG = 0.56 V  
### Power and Saturation Verification
### 1. Power Verification

Given:
VDD = 1.2 V  
ID = 200 µA  

Power:
P = VDD × ID  
P = 1.2 × 200 × 10⁻⁶  
P = 0.24 mW  
Since 0.24 mW < 0.4 mW  
Power specification satisfied.

### 2. NMOS Saturation Check

Condition:
VDS ≥ VOV  

Given:
VOV = 0.25 V  
VD = 0.8 V  
VS = 0.2 V  
VDS = 0.8 − 0.2 = 0.6 V  
0.6 V ≥ 0.25 V  
NMOS in saturation.

### 3. PMOS Saturation Check
Condition:
VSD ≥ VOV  

Given:
VOV = 0.25 V  
VS = 1.2 V  
VD = 0.8 V  
VSD = 1.2 − 0.8 = 0.4 V  
0.4 V ≥ 0.25 V   
PMOS in saturation.

<img width="1482" height="698" alt="image" src="https://github.com/user-attachments/assets/44294c54-d572-4978-8e3c-e4c4adc24e09" />

# DC Sweep Analysis
<img width="1903" height="768" alt="image" src="https://github.com/user-attachments/assets/7ed9ead7-4b08-4c6f-9307-97ae23ab2267" />
From the DC sweep graph:
- Output remains near 0 V until Vin crosses threshold.
- After threshold, Vout increases rapidly.
- Proper biasing ensures operation in saturation for amplification.
- The region where the curve is smooth and approximately linear indicates proper amplifier operation.

Thus, DC Sweep helps verify correct biasing and region of operation before performing AC or transient analysis.
# Transient Analysis
<img width="1910" height="829" alt="image" src="https://github.com/user-attachments/assets/0d539043-e116-4903-a16f-c47d3b0eeee9" />
## Theoretical Gain

gm = 2ID / VOV  
gm = (2 × 200 × 10⁻⁶) / 0.25  
gm = 1.6 × 10⁻³ S  

ro = 1 / (λ ID)  
ro = 1 / (0.1 × 200 × 10⁻⁶)  
ro = 50 kΩ  

(ro1 || ro2) = 25 kΩ  

Av = - gm (ro1 || ro2) / (1 + gm RS)
Av = - (1.6 × 10⁻³ × 25 × 10³) / (1 + 1.6 × 10⁻³ × 1 × 10³)
Av = -40 / 2.6  
Av = -15.38 V/V  

Av(dB) = 20 log(15.38)  
Av(dB) = 23.74 dB  

## Practical Gain (From Transient)

Av = ΔVout / ΔVin  
Av = (0.992 − 0.423) / (0.819 − 0.8003)
Av = 0.569 / 0.0187  
Av = 6.309 V/V  

Av(dB) = 20 log(6.309)  
Av(dB) ≈ 16 dB  
The practical gain (16 dB) is lower than the theoretical gain (23.74 dB) because:

- Theoretical calculation assumes ideal large output resistance (ro).
- In simulation, channel length modulation reduces ro.
- Parasitic capacitances and accurate BSIM model parameters reduce effective gain.
- Source degeneration (RS) further lowers the overall voltage gain.

# AC Analysis
<img width="1904" height="761" alt="image" src="https://github.com/user-attachments/assets/cc08549c-7730-4b3b-80b3-ecd62f104316" />
<img width="1910" height="814" alt="image" src="https://github.com/user-attachments/assets/fa3fda83-2f89-47bf-af96-22ff5688ab1c" />

Bandwidth is measured at:
Av(mid) − 3 dB
= 16.473 − 3  
= 13.473 dB
fH (upper cutoff frequency) ≈ 371.525 MHz  
fL (lower cutoff frequency) ≈ 0 Hz  

Therefore:
Bandwidth (BW) ≈ 371.525 MHz
From AC analysis plot
At frequency ≈ 4.03 GHz  
Magnitude ≈ 4.54 mdB ≈ 0 dB  

Therefore,
UGB ≈ 4.03 GHz

UGB ≈ Av(midband) × f3dB
Midband Gain ≈ 16 dB  
 
Av ≈ 15.384
f3dB ≈ 371.5 MHz  
Now,
UGB = Av × f3dB  
UGB = 15.384 × 371.5 MHz  
UGB ≈ 5.7 GHz  

From direct 0 dB crossing:
UGB ≈ 4.03 GHz  
From Gain–Bandwidth product:
UGB ≈ 5.7 GHz  

The small difference occurs due to:
- Non-ideal multi-pole behavior
- Parasitic capacitances
- Non-dominant poles

# CIRCUIT 2
# DC Analysis
<img width="579" height="432" alt="image" src="https://github.com/user-attachments/assets/47ef5df8-8cc9-4037-bc75-eabc65034644" />

This circuit is a **Cascode Common Source (CS) Amplifier with PMOS active load**.
## Cascode Structure (M2–M3)

- M2 acts as the input transistor (Common Source).
- M3 acts as the cascode transistor.
- The cascode transistor keeps VDS of M2 nearly constant.

Special advantages:
- Significantly increases output resistance (Rout).
- Reduces Miller effect.
- Improves gain and bandwidth.
- Enhances frequency performance.
  
## DC Operating point and Design Calculation
<img width="1280" height="645" alt="image" src="https://github.com/user-attachments/assets/41b6c467-6f08-4647-9492-e0e4427b7876" />

# M1 – NMOS (Input Transistor)
Current Equation Used
ID = (μ Cox / 2) (W/L) (VOV)²
Vout = VDD / 2
=1.2 / 2 = 0.6 V 

| Parameter | Equation | Substitution | Result |
|------------|----------|--------------|--------|
| VGS | VOV + VTN | 0.2 + 0.366 | 0.566 V |
| VS | Assumed | — | 0.3 V |
| VG | VGS + VS | 0.566 + 0.3 | 0.866 V |
| VDS | Vout − VS | 0.6 − 0.3 | 0.3 V |
| Saturation Check | VDS ≥ VOV | 0.3 ≥ 0.2 | Saturation |
| Width (Initial) | From ID eqn | — | 7.805 µm |
| Width (Final) | Adjusted for ID = 200 µA | — | 34.305 µm |

# M2 – NMOS (Cascode Transistor)

| Parameter | Equation | Substitution | Result |
|------------|----------|--------------|--------|
| VGS | VOV + VTN | 0.2 + 0.366 | 0.566 V |
| VG2 | = VGS | — | 0.566 V |
| VDS | ≈ 0.3 V | — | 0.3 V |
| Saturation Check | VDS ≥ VOV | 0.3 ≥ 0.2 | Saturation |
| Width (Final) | Same current as M1 | — | 34.305 µm |

# M3 – PMOS (Active Load)

| Parameter | Equation | Substitution | Result |
|------------|----------|--------------|--------|
| VSG | VOV + |VTP| | 0.2 + 0.39 | 0.59 V |
| VG | VDD − VSG | 1.2 − 0.59 | 0.61 V |
| VSD | VDD − Vout | 1.2 − 0.6 | 0.6 V |
| Saturation Check | VSD ≥ VOV | 0.6 ≥ 0.2 | Saturation |
| Width (Initial) | From ID eqn | — | 18.473 µm |

# Final Fixed Width Design

| Transistor | Width (µm) |
|------------|------------|
| M1 (NMOS)  | 34.305 µm  |
| M2 (NMOS)  | 34.305 µm  |
| M3 (PMOS)  | 44.813 µm  |

All widths are calculated to maintain ID = 200 µA with VOV = 0.2 V.

# Transient Analysis
<img width="1904" height="832" alt="image" src="https://github.com/user-attachments/assets/ca9547f9-7ce6-42dc-bd58-84731a0beedb" />
## Practical Gain Calculation

| Parameter | Expression | Substitution | Result |
|------------|------------|--------------|--------|
| ΔVout | Vout(max) − Vout(min) | 627.83 mV − 585.94 mV | 41.89 mV |
| ΔVin | Given | 20 mV | 20 mV |
| Av | ΔVout / ΔVin | 41.89 / 20 | 2.094 V/V |
| Av(dB) | 20 log(Av) | 20 log(2.094) | 6.421 dB |

## Theoretical Gain Calculation
### Step 1: Transconductance (gm1)

| Parameter | Expression | Substitution | Result |
|------------|------------|--------------|--------|
| gm1 | 2ID / VOV | (2 × 200×10⁻⁶) / 0.2 | 2 × 10⁻³ S |

### Step 2: Output Resistance

| Transistor | Expression | Substitution | Result |
|------------|------------|--------------|--------|
| NMOS (ro1, ro2) | 1 / (λ ID) | 1 / (0.1 × 200×10⁻⁶) | 50 kΩ |
| PMOS (ro3) | 1 / (λ ID) | 1 / (0.12 × 200×10⁻⁶) | 41.66 kΩ |

### Step 3: Effective Output Resistance

ro_eff = (ro1 || ro3)
ro_eff = (50k × 41.66k) / (50k + 41.66k)
ro_eff ≈ 22.727 kΩ

### Step 4: Voltage Gain (With Source Degeneration)

Av = − gm1 × ro_eff / (1 + gm1 ro2)

Substitute:
Av = − (2×10⁻³ × 22.727×10³) / (1 + 2×10⁻³ × 50×10³)
Av = − 45.45 / (1 + 100)
Av ≈ − 0.45 V/V

| Parameter | Result |
|------------|--------|
| Av (Linear) | 0.45 V/V |
| Av (dB) | 20 log(0.45) = −6.935 dB |

### Final Comparison

| Type | Gain (V/V) | Gain (dB) |
|------|------------|------------|
| Practical | 2.094 | 6.421 dB |
| Theoretical | 0.45 | −6.935 dB |

# AC Analysis
<img width="1904" height="800" alt="image" src="https://github.com/user-attachments/assets/7284f9ec-2fd7-4857-b3ca-875202e24c35" />
### 1. Cutoff Frequencies
-Lower cutoff frequency:
fL = 0 Hz  
-Upper cutoff frequency (from AC plot):
fH = 136.405 MHz  

### 2. Midband Gain
Midband Gain = 7.857 dB  

Convert to linear:
Av(mid) = 10^(7.857/20)  
Av(mid) ≈ 2.094 V/V  
3 dB below midband gain:
7.857 − 3 = 4.857 dB  
From AC plot:
BW = 136.405 MHz  

<img width="1891" height="785" alt="image" src="https://github.com/user-attachments/assets/0bcfbb3c-699f-4eb9-8d54-d52c756299d6" />
### 4. Unity Gain Bandwidth (UGB)

Using Gain–Bandwidth Product:

UGB = Av(mid, linear) × f3dB  
UGB = 2.094 × 136.405 MHz  
UGB ≈ 285.63 MHz  
0 dB frequency ≈ 316.227 MHz  


