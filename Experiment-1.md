## Experiment 1

## DC, AC and Transient Analysis of Common Source (CS) Amplifier  

##  Aim
To design a Common Source (CS) amplifier using NMOS transistor in TSMC 180nm technology library in LTspice and perform DC, AC, and Transient analysis.
Design Specifications
  - Technology: 180 nm (TSMC)
  - VDD = 2 V
  - Power Budget = 1.2m W
Parameters to be Extracted
  - DC Operating Point
  - Gain
  - Bandwidth
  - Power
      
## Common-Source (CS) Amplifier
# Introduction
  The Common-Source (CS) amplifier is a single-stage voltage amplifier built using a MOSFET operating in the saturation region. It is the most fundamental MOSFET amplifier configuration used in analog CMOS circuits.
  
In a MOSFET, current flows between the drain and source terminals, and this drain current (ID) is controlled by the gate-to-source voltage (VGS). The gate draws approximately zero DC current because of its very high input impedance. In a Common-Source (CS) amplifier configuration, the input signal is applied at the gate, the output is taken from the drain, and the source is common (usually grounded). Amplification occurs because a small change in VGS produces a proportional change in drain current (ID), which creates a larger voltage variation across the drain load resistor. As a result, a small input voltage signal at the gate is converted into a larger output voltage signal at the drain.

This document covers a common implementations of the CS amplifier:
  -CS Amplifier with a Resistor Load

# CS Amplifier with a Resistor Load
# Large-Signal Operation
The large-signal behavior of the Common-Source (CS) amplifier describes how the circuit responds as the input voltage (VIN) varies over a wide range.

  - When **VIN is close to 0 V**, the gate-to-source voltage (VGS) is less than the threshold voltage (VTH). The MOSFET remains in the **cutoff region**, resulting in **ID ≈ 0**. Since no current flows through the load resistor (RD or RL), there is no voltage drop across it, and the output voltage (VOUT) remains approximately equal to **VDD**. 
  - As **VIN increases and approaches VTH**, the MOSFET begins to turn on. A small drain current (ID) starts flowing, producing a small voltage drop across the load resistor. Consequently, **VOUT begins to decrease slightly** from VDD.  
  - When **VIN exceeds VTH sufficiently**, the MOSFET enters the **saturation region** (provided VDS ≥ VGS − VTH). In this region, the transistor operates as a voltage-controlled current source. The amplifier provides proper voltage amplification, and the output varies inversely with the input.  
  - As **VIN increases further**, the drain current increases significantly. If VDS becomes smaller than (VGS − VTH), the MOSFET transitions into the **linear (triode) region**. In this region, the device no longer behaves as an ideal amplifier, and VOUT drops further due to increased current through the load resistor.  
  Since a MOSFET provides effective amplification only when operating in the **saturation region**, the useful operating range of the CS amplifier is limited to input voltage values that keep the transistor in saturation.
# Circuit Diagram
<img width="718" height="658" alt="LSMM" src="https://github.com/user-attachments/assets/06264d66-b84a-4185-8b44-61c0fe27b230" />

## Small-Signal Operation

Small-signal operation describes the behavior of the Common-Source (CS) amplifier when a small AC signal is applied around the DC operating point (Q-point). In this analysis, the MOSFET is assumed to be biased in the **saturation region**.

- A small variation in input voltage (vin) produces a small variation in gate-to-source voltage (vgs).

- This small change in vgs causes a proportional change in drain current (id), given by:
  id = gm · vgs
  where gm is the transconductance of the MOSFET.

- The variation in drain current flows through the load resistor (RD), producing a corresponding change in output voltage:
 vout = − id · RD
- Substituting id:
  vout = − gm · vgs · RD
- Therefore, the small-signal voltage gain (Av) is:
  Av = vout / vin  
  Av = − gm RD
The negative sign indicates a **180° phase shift** between input and output.

In small-signal analysis:
- The MOSFET behaves as a voltage-controlled current source.
- The DC supply (VDD) is treated as AC ground.
- The gain depends primarily on gm and RD.
- Larger gm (achieved by increasing W or ID) results in higher gain.
- Larger RD increases gain but reduces bandwidth.

Thus, in small-signal operation, the CS amplifier provides linear amplification around the operating point, as long as the MOSFET remains in the saturation region.

# Small Signal Model
<img width="809" height="213" alt="SSM" src="https://github.com/user-attachments/assets/fc601d3e-d237-4244-bf83-703da536151d" />

## DC Analysis of CS Amplifier with a Resistor Load
## Procedure

1. **Create a New Experiment Workspace**  
   Open LTspice and create a new schematic file for the experiment.
2. **Add Technology Library**  
   Insert a SPICE directive by clicking on the `.op` / `.lib` option from the toolbar.  
   Enter the following command:
   .lib tsmc018.lib
   This command loads the BSIM3 MOSFET model.  
   If the library file is stored in another location, specify the full file path in the command.
3. **Add the MOSFET**  
   - Place the NMOS transistor (NMOS4) in the schematic.  
   - Change the name of the transistor to `CMOSN`.
4. **Current Calculation Based on Power Budget**
   Since supply voltage (VDD) and power budget (P) are given, the maximum allowable drain current can be calculated as:
   I = P / V
5. **Aspect Ratio (W/L) Selection**
   - Choose different combinations of Width (W) and Length (L).  
   - Calculate drain current using the saturation equation:
     ID = (1/2) μn Cox (W/L) (VGS − VTH)²
   - Adjust W and L until the desired current is achieved.
6. **Perform Analyses**
   After selecting suitable W and L values:
   - Perform DC Analysis
   - Perform Transient Analysis
   - Perform AC Analysis
   - 
## DC Operating Point

To perform DC Operating Point analysis:
  1. Go to **Simulate → Configure Analysis → DC Operating Point**
  2. Add the `.op` command in the schematic workspace.
  3. Click on the **Run (Play)** button to start simulation.
  4. The simulation generates a SPICE Output Log file.
  5. To view voltages and currents:
     - Go to **View → SPICE Output Log**
<img width="527" height="383" alt="dc " src="https://github.com/user-attachments/assets/5b6a3244-4d2d-4955-a4d6-be948a576267" />
# Calculation
## Design Calculations

# Given:
Some values taken from tsmc018.lib
VDD = 2 V  
Power ≤ 1.2 mW  
CL = 0.7 pF  
L = 180 nm  
VTH = 0.366 V  
μn = 273.809 cm²/Vs  
tox = 4.1 × 10⁻⁹ m  

Take: ID = 200 µA  

# Drain Resistor Calculation

Vout = VDD − ID RD  
For maximum swing:
VDS = VDD / 2  
VDS = 1 V  
So,
1 = 2 − ID RD  
1 = 2 − (200 × 10⁻⁶) RD  
1 = ID RD  
RD = 1 / (200 × 10⁻⁶)  
RD = 5 × 10³ Ω  
RD = 5 kΩ  

# Power Verification

P = VDD ID  
P = 2 × 200 × 10⁻⁶  
P = 4 × 10⁻⁴ W  
P = 0.4 mW  
Since: 0.4 mW ≤ 1.2 mW 

# Oxide Capacitance Calculation

εox = ε0 εr  
ε0 = 8.854 × 10⁻¹²  
εr = 3.453  
εox = 8.854 × 10⁻¹² × 3.453  
Cox = εox / tox  
Cox = (8.854 × 10⁻¹² × 3.453) / (4.1 × 10⁻⁹)  

# Width (W) Calculation

Drain current equation (Saturation):
ID = (μn Cox / 2) (W / L) (VGS − VTH)²  
Substitute:
200 × 10⁻⁶  = (273.809 × 10⁻⁴ × Cox / 2) (W / 180 × 10⁻⁹) (0.9 − 0.366)²  
Solving for W:
W ≈ 1.07 µm  
After adjustment: 
For: W = 1.07 µm → ID ≈ 165 µA  
For: W = 1.377 µm → ID ≈ 185 µA 
For: W = 1.508 µm → ID ≈ 200 µA

<img width="647" height="434" alt="op" src="https://github.com/user-attachments/assets/270ccecb-1732-4911-8df5-7a78fee2cab1" />

# Effect of Channel Width (W) on Drain Current (ID)

| Width (W) in µm | Drain Current (ID) in µA | Observation |
|-----------------|--------------------------|-------------|
| 1.07 µm        | ≈ 165 µA                 | Lower width results in lower drain current |
| 1.377 µm       | ≈ 185 µA                 | Moderate increase in width increases current |
| 1.508 µm       | ≈ 200 µA                 | Higher width achieves target drain current |

Drain current (ID) is directly proportional to the channel width (W).
As W increases:
- The (W/L) ratio increases.
- The channel area increases.
- More charge carriers flow through the channel.
- Drain current increases proportionally.
# Effect of Drain Resistor on Q point
As the drain resistance (RD) increases, the drain-to-source voltage (VDS) decreases due to the increased voltage drop across the drain resistor for a constant drain current.
## Variation of VDS with Drain Resistance (RD)

| S.No | Drain Resistance (RD) | VDS (Drain-to-Source Voltage) |
|------|-----------------------|-------------------------------|
| 1    | 2.2 kΩ                | 1.528 V                       |
| 2    | 3 kΩ                  | 1.369 V                       |
| 3    | 5 kΩ                  | 0.998 V  (required)           |
| 4    | 6 kΩ                  | 0.828 V                       |

## DC Sweep Analysis of Transfer Characteristics (Vout vs Vin)
- For low Vin (< VTH ≈ 0.366 V), the MOSFET is in cutoff region. Drain current is nearly zero, so Vout remains close to VDD (≈ 2 V).
- As Vin increases beyond VTH, the MOSFET enters saturation and drain current increases. This causes a voltage drop across the 5 kΩ drain resistor, resulting in a decrease in Vout.
- In the middle region, the curve shows a steep negative slope. This is the active amplification region where small changes in Vin produce large changes in Vout, indicating high voltage gain.
- At higher Vin, the transistor conducts strongly, VDS reduces significantly, and Vout approaches a low voltage (~0.2 V), limiting further amplification.
<img width="1895" height="847" alt="dc sweep" src="https://github.com/user-attachments/assets/c3791e5f-ad22-4331-80d8-a4510c132e23" />

## Transient Analysis
<img width="1905" height="828" alt="trans" src="https://github.com/user-attachments/assets/d47764ba-0363-4767-9fd1-960ccbde8457" />
# Gain Calculation 
# Given Parameters

| Vout(max) | — | 1.02 V |
| Vout(min) | — | 0.970 V |
| Vin(max) | — | 0.909 V |
| Vin(min) | — | 0.890 V |

# Practical Gain Calculation
| Quantity | Formula | Calculation | Result |
|----------|----------|-------------|--------|
| ΔVout | Vout(max) − Vout(min) | 1.02 − 0.970 | 0.050 V |
| ΔVin | Vin(max) − Vin(min) | 0.909 − 0.890 | 0.019 V |
| Voltage Gain (Av) | ΔVout / ΔVin | 0.050 / 0.019 | 2.654 |
| Gain in dB | 20 log10(Av) | 20 log10(2.654) | 8.478 dB |

# Theoretical Gain Calculation
| Quantity | Formula | Calculation | Result |
|----------|----------|-------------|--------|
| Overdrive Voltage | Vov = VGS − VTH | 0.9 − 0.366 | 0.534 V |
| Transconductance | gm = 2ID / Vov | (2 × 200×10⁻⁶) / 0.534 | 0.000749 S |
| Voltage Gain | Av = gm × RD | 0.000749 × 5000 | 3.745 |
| Gain in dB | 20 log10(Av) | 20 log10(3.745) | 11.46 dB |

The transient analysis verifies:
  - Proper DC biasing
  - Small-signal amplification
  - Inversion property of CS amplifier
  - Stable operation at 1 kHz

## AC Analysis without bypass capacitor
<img width="1899" height="830" alt="wocap" src="https://github.com/user-attachments/assets/9e10f9e5-a3fe-45bc-9b3f-8956742af479" />
# Frequency Analysis (Without Bypass Capacitor)

| Type        | Midband Gain (dB) | -3 dB Gain (dB) | Bandwidth Frequency |
|------------|-------------------|-----------------|--------------------|
| Practical  | 8.833 dB          | 5.833 dB        | 52.329 GHz         |
| Theoretical| 8.478 dB          | 5.478 dB        | 59.113 GHz         |

The theoretical gain assumes ideal small-signal behavior (Av = gmRD) and neglects channel length modulation, output resistance (ro), parasitic capacitances, and device non-linearities. In practical simulation, these second-order effects, along with finite output resistance, intrinsic capacitances (Cgs, Cgd), and loading effects, reduce the effective gain and slightly shift the bandwidth. Therefore, the simulated (practical) results differ slightly from the ideal theoretical values.

## AC Analysis with bypass capacitor
<img width="1907" height="804" alt="wcap" src="https://github.com/user-attachments/assets/bb7c364d-3f11-4751-9b68-0f8f51be47ce" />
## Frequency Analysis (With Bypass Capacitor)

| Type        | Midband Gain (dB) | -3 dB Gain (dB) | Bandwidth Frequency |
|------------|-------------------|-----------------|--------------------|
| Practical  | 9.465 dB          | 6.465 dB        | 35.746 MHz         |

# Observations
- The midband gain increases when the bypass capacitor is used.
- The bandwidth significantly reduces when the bypass capacitor is added.
- Without the capacitor, gain is lower but high-frequency response extends further.
- With the capacitor, gain improves but high-frequency performance decreases.

# Reason for the Difference
Without the bypass capacitor, the source resistor remains in the AC signal path, introducing **source degeneration**. This reduces the effective transconductance and lowers the voltage gain.

When a bypass capacitor is added across the source resistor:
- The source resistor is effectively shorted for AC signals.
- Source degeneration is eliminated.
- Effective transconductance (gm) increases.
- Voltage gain increases.

However, the bypass capacitor introduces an additional reactive element into the circuit:
- It forms an RC time constant.
- This creates a pole in the frequency response.
- As a result, the bandwidth decreases.

# Conclusion
Adding a bypass capacitor increases gain by removing AC degeneration but reduces bandwidth due to additional pole formation. This demonstrates the gain–bandwidth tradeoff in amplifier design.

## Inference
- The term **180 nm technology** specifies the minimum channel length that can be fabricated; however, transistors with lengths greater than 180 nm can also be easily manufactured.
- At very small channel lengths (L), the saturation drain current no longer varies linearly with width (W). The deviation from the ideal current equation occurs due to short-channel effects, channel length modulation, and other second-order effects.
- For larger values of L, the linear proportionality between width (W) and drain current is better maintained, matching the long-channel current model.
- Care must be taken while selecting the drain resistance (RD), since improper values can push the MOSFET out of saturation. Techniques such as source degeneration, voltage-divider biasing, and source bypass filtering can improve bias stability and reduce sensitivity.
- In the absence of coupling or bypass capacitors, there is no lower cutoff frequency. However, the upper cutoff frequency still exists due to intrinsic parasitic capacitances (Cgs, Cgd), which are inherent to the MOSFET.
- The drain resistance directly influences the voltage gain (Av = gmRD). Increasing RD increases gain, but beyond a certain limit it may drive the transistor toward the edge of saturation or into the linear region, which is undesirable for proper CS operation.
- A trade-off can be made by reducing drain current to achieve higher gain while managing power consumption.
- In the current-source load configuration, the drain characteristics exhibit a more linear behavior due to the active load, while the transfer characteristics resemble those of the resistive-load CS amplifier.
- For 180 nm technology, it is possible to achieve the required operating conditions by adjusting VGS to 0.9 V. Through iterative design, a suitable width of approximately 1.508 µm was obtained for RD = 5 kΩ.


