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

# Circuit 3
# Common-Source Amplifier with Active PMOS Load and Source Degeneration

## Introduction

This circuit represents a CMOS common-source amplifier implemented using TSMC 0.18 µm technology. The topology consists of:
- **M1 (NMOS)** – Main amplifying transistor  
- **M2 (NMOS)** – Source degeneration transistor  
- **M3 (PMOS)** – Active load transistor

 A diode-connected MOSFET has:
Gate connected to Drain
Therefore:VGS = VDS

Why it is used:
-Acts like a nonlinear resistor
-lways operates in saturation (if VGS > VTH)
-Provides bias stability
-Increases output resistance compared to resistor load


Small-Signal Model
A diode-connected NMOS behaves like:
1/gm in parallel with ro
So its effective resistance ≈ 1/gm (if gm ≫ 1/ro)
This reduces gain compared to a current source load but improves linearity and bias stability.

# DC Analysis
<img width="740" height="596" alt="image" src="https://github.com/user-attachments/assets/27674bba-aec6-4449-b5b7-2141986fa7c9" />
Given:
ID = 200 µA
VOV = 0.2 V
VDD = 1.2 V
VTHn = 0.366 V
|VTHp| = 0.39 V
λ ≈ 0.1 V⁻¹

## M3 (Diode-Connected NMOS)

VGS3 = VTHn + VOV
VGS3 = 0.366 + 0.2
VGS3 = 0.566 V

Since diode connected:
VS1 = VGS3 = 0.566 V

Check saturation:
VDS3 = VGS3 = 0.566 V
Condition:
VDS3 ≥ VOV 
0.566 ≥ 0.2  
M3 is in saturation.

## M1 (Common Source NMOS)

To maintain same VOV:

VGS1 = VTHn + VOV
VGS1 = 0.366 + 0.2
VGS1 = 0.566 V
VS1 = 0.566 V
Therefore:
Vin = VGS1 + VS1
Vin = 0.566 + 0.566
Vin = 1.132 V  

Now check saturation of M1.
For saturation:
VDS1 ≥ VOV
VDS1 = Vout − VS1

## M2 (PMOS Load)

For PMOS:
VSG2 = |VTHp| + VOV
VSG2 = 0.39 + 0.2
VSG2 = 0.59 V

Check saturation:
VSD2 ≥ VOV
If Vout ≈ 0.8 V:
VSD2 = VDD − Vout
VSD2 = 1.2 − 0.8
VSD2 = 0.4 V

0.4 ≥ 0.2  
PMOS is in saturation.

# CMOS Width Calculation (VOV = 0.1 V)

## Given Parameters

ID = 200 µA  
VOV = 0.1 V  
L = 0.18 µm = 0.18 × 10⁻⁶ m  
µn = 273.809 cm²/Vs = 0.02738 m²/Vs  
µp = 115.689 cm²/Vs = 0.01157 m²/Vs  
Tox = 4.1 × 10⁻⁹ m  
εr = 3.9  
ε0 = 8.854 × 10⁻¹² F/m  

## Oxide Capacitance

Cox = (εr ε0) / Tox  
Cox = (3.9 × 8.854 × 10⁻¹²) / (4.1 × 10⁻⁹)  
Cox ≈ 8.42 × 10⁻³ F/m²  

## Drain Current Equation (Saturation)

ID = (1/2) µ Cox (W/L) VOV²  
Rearranging for W:
W = (2 ID L) / (µ Cox VOV²)

#  NMOS Width Calculation

Wn = (2 × 200×10⁻⁶ × 0.18×10⁻⁶)  
     / (0.02738 × 8.42×10⁻³ × (0.1)²)

Numerator:
= 7.2 × 10⁻¹¹  
Denominator:
= 2.305 × 10⁻⁶  
Wn = 3.12 × 10⁻⁵ m  
Wn = 31.2 µm  

###  NMOS Width

Wn ≈ 31 µm  

(M1 and M3 if identical)

#  PMOS Width Calculation

Wp = (2 × 200×10⁻⁶ × 0.18×10⁻⁶)  
     / (0.01157 × 8.42×10⁻³ × (0.1)²)

Denominator:
= 9.74 × 10⁻⁷  
Wp = 7.39 × 10⁻⁵ m  
Wp = 73.9 µm  
### PMOS Width
Wp ≈ 74 µm 

# Final Device Sizing
| Transistor | Width (µm) | Length (µm) |
|------------|------------|-------------|
| NMOS (M1, M3) | 31 | 0.18 |
| PMOS (M2) | 74 | 0.18 |

## Design Notes
• PMOS width is larger due to lower mobility  
• Ratio Wp/Wn ≈ 2.3  
• All devices biased at ID = 200 µA  
• Designed for VOV = 0.1 V (low-voltage 1.2 V operation)

# Transient Analysis
<img width="1915" height="845" alt="image" src="https://github.com/user-attachments/assets/37864148-428f-4cb1-97f7-3902c6be3c34" />
# Theoretical Calculations

## Transconductance

gm1 = gm2 = (2ID / VOV)
gm = (2 × 200×10⁻⁶) / 0.2  
gm = 2 × 10⁻³ S  
gm = 2 mS  

## Output Resistance

ro2 = 1 / (λ ID)
ro = 1 / (0.1 × 200×10⁻⁶)  
ro = 1 / (20×10⁻⁶)  
ro = 50 kΩ  

## Voltage Gain

Av = - gm1 × ro2/(1+gm1/gm3)  
Av = - (2mS × 50kΩ)/2  
Av = -50 V/V  

Magnitude:
|Av| = 50  

In dB:
Av(dB) = 20 log(50)  
Av(dB) = 33.97 dB  

You calculated:
Av= - gm1* ro2/(1+gm1/gm3)
Av = 50  

Av(dB) = 20 log(50)  
Av(dB) = 33.97 dB  

(This corresponds to effective gain reduction due to degeneration/loading.)
## Practical gain 
Av = ΔVout / ΔVin
Av = 730.82-559.02/20
Av = 8.59 V/V

In dB , AvdB = 20 log(8.59)
          = 18.679 dB
| Parameter | Theoretical Gain | Practical Gain |
|------------|------------------|----------------|
| Av (V/V) | 50 V/V | 8.59 V/V |
| Av (dB) | 33.97 dB | 18.679 dB |

# AC Analysis
<img width="1888" height="777" alt="image" src="https://github.com/user-attachments/assets/e8e34ea1-c0bc-4030-988e-7a1311661de3" />
Midband Gain:

Av = 18.630 dB  
3 dB bandwidth level:
18.630 − 3 = 15.630 dB  
Frequency at 15.630 dB:
f3dB = 300.3852 MHz  

# Unity Gain Bandwidth
<img width="1915" height="810" alt="image" src="https://github.com/user-attachments/assets/0103088f-bf9c-46c9-9960-8fa26ba751a5" />

UGB (0 dB frequency) ≈ 5.139 GHz  

Using approximation:
UGB = Av(linear) × f3dB  
Convert gain to linear:
Av(linear) = 10^(18.630/20)  
Av(linear) ≈ 8.59  

UGB ≈ 8.59 × 300.3852 MHz  
UGB ≈ 2.58 GHz  

Higher cutoff Frequency, fH= 300.385MHz

Lower cutoff frequency, fL=0Hz

• Smaller channel length → larger λ → lower ro → lower gain  
• Increasing L reduces λ and improves gain  
• In 180 nm technology, CLM effect is noticeable

# Comparison of Three MOSFET Amplifier Circuits (180 nm CMOS)

##  Performance Comparison Table

| Parameter | Circuit 1: CS + PMOS Load + RS | Circuit 2: Cascode CS | Circuit 3: CS + Diode Load |
|------------|--------------------------------|------------------------|----------------------------|
| Topology | Common Source + Active Load + Source Degeneration | Cascode CS + PMOS Load | CS + Diode-Connected Load |
| ID | 200 µA | 200 µA | 200 µA |
| VDD | 1.2 V | 1.2 V | 1.2 V |
| Power | 0.24 mW | 0.24 mW | 0.24 mW |
| Theoretical Gain (dB) | 23.74 dB | −6.93 dB (with degeneration) | 33.97 dB |
| Practical Gain (dB) | 16 dB | 6.42 dB | 18.68 dB |
| Midband Gain (AC) | 16.47 dB | 7.857 dB | 18.63 dB |
| Bandwidth | 371.5 MHz | 136.4 MHz | 300.38 MHz |
| UGB (Simulated) | 4.03 GHz | 316 MHz | 5.139 GHz |
| Output Resistance | Moderate | High (cascode effect) | Lower (due to diode load) |
| Linearity | Improved (RS present) | Good | Moderate |
| Stability | Good | Very Good | Good |

# Applications (Brief)

## Circuit 1 – CS with PMOS Active Load + Source Degeneration
- Audio and sensor pre-amplifiers  
- Analog front-end stages  
- ADC driver (low–moderate speed)  
- Biomedical signal amplification  
- General low-power CMOS amplification  

## Circuit 2 – Cascode CS Amplifier
- RF and high-frequency amplifiers  
- Operational amplifier gain stages  
- Current mirrors and precision bias circuits  
- Low-noise amplifiers (LNA)  
- High-output-resistance applications  

## Circuit 3 – CS with Diode-Connected Load
- Simple voltage amplification stages  
- On-chip bias circuits  
- Compact low-power analog blocks  
- Current-to-voltage converters  
- Basic CMOS analog building blocks  

**Summary:**  
Circuit 1 → Balanced performance  
Circuit 2 → High-frequency/high-output resistance  
Circuit 3 → Simple and compact design  

#  Result

1. All three circuits operate within power specification (≤ 0.4 mW).
2. Circuit 3 gives the highest practical midband gain (~18.6 dB).
3. Circuit 1 provides balanced performance with good bandwidth (~371 MHz).
4. Circuit 2 (Cascode) improves output resistance but practical gain remains low.
5. Circuit 3 achieves highest UGB (~5.1 GHz).
6. Source degeneration in Circuit 1 improves linearity but reduces gain.
7. Cascode structure increases theoretical output resistance.
8. Diode-connected load reduces gain but simplifies biasing.
9. Gain-bandwidth trade-off clearly observed across circuits.
10. All circuits validate 180 nm CMOS analog design principles.


# Inference
# Interpretation of Results

1. All three circuits successfully operate at 1.2 V supply with ID = 200 µA and satisfy the power constraint (< 0.4 mW).
2. Practical gain is lower than theoretical gain in all circuits due to:
   - Channel Length Modulation (finite ro)
   - Parasitic capacitances
   - Short-channel effects (180 nm technology)
3. Circuit 1 (CS + RS + PMOS load) shows balanced performance:
   - Moderate gain
   - Wide bandwidth
   - Improved linearity due to source degeneration
4. Circuit 2 (Cascode) increases output resistance theoretically, but limited voltage headroom in 1.2 V supply reduces practical gain.
5. Circuit 3 (Diode-connected load) provides higher gain than Circuit 2 and simple biasing, but gain is limited by 1/gm load behavior.
6. Gain–Bandwidth trade-off is clearly observed:
   - Higher gain reduces bandwidth.
   - Lower gain increases bandwidth.
7. Cascode reduces Miller effect and improves high-frequency behavior, but consumes voltage headroom.
8. Source degeneration improves stability and linearity but reduces voltage gain.
9. Smaller channel length (180 nm) increases λ, reducing output resistance and gain.
10. Overall, practical performance confirms real CMOS non-ideal effects and validates analog design principles under low-voltage operation.
