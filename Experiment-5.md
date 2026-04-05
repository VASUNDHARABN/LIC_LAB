# Experiment 5:
# Circuit-1 Voltage Follower (Buffer)

## Aim
To design and analyze a voltage follower circuit using an operational amplifier and verify that the output voltage follows the input voltage (unity gain).

---

## Introduction
A voltage follower is a fundamental operational amplifier (op-amp) configuration that provides unity gain. It is widely used in analog circuits for buffering, impedance matching, and signal isolation between different stages of a system.

In practical electronic systems, directly connecting a source to a load can cause signal distortion due to loading effects. The voltage follower eliminates this issue by acting as an interface, ensuring that the input signal is transferred to the output without any loss in amplitude.

---

## Theory
A voltage follower is a special case of a non-inverting amplifier where the output is directly fed back to the inverting terminal.

General gain formula of non-inverting amplifier:
Av = 1 + (Rf / R1)

For voltage follower:
Rf = 0 and R1 = ∞

So,
Av = 1

Therefore,
Vout = Vin

### Characteristics:
- Unity gain (Av = 1)
- No phase inversion
- Very high input impedance
- Very low output impedance
- Used for impedance matching

---

## Working Principle
The working of a voltage follower is based on negative feedback.

- The input signal is applied to the non-inverting terminal (+).
- The output is directly connected to the inverting terminal (−).
- Due to the very high open-loop gain of the op-amp, even a small difference between the inputs drives the output.
- The negative feedback forces the inverting input voltage to become equal to the non-inverting input voltage.

Thus,
V− = V+ = Vin

Hence,
Vout = Vin

This condition is called a virtual short.

---

## Circuit Design
- Input is applied to non-inverting terminal (+)
- Output is directly connected to inverting terminal (−)
- No resistors are used
-Device current → current through simple elements (R, V, etc.)
-Subckt current → current entering/leaving a subcircuit block (like op-amp)
---
## Circuit Diagram
<img width="808" height="463" alt="image" src="https://github.com/user-attachments/assets/311cdfff-2989-4935-bd4b-4033ae829907" />


## Design Calculation
Given:
Vin(p-p) = 10 V  
Vcc = 13 V  
RL = 4.7 kΩ  

Gain:
Av = 1
### DC Analysis
<img width="1498" height="672" alt="image" src="https://github.com/user-attachments/assets/bae4ba49-dad8-4bc7-aaae-66d405db06b2" />

Output:
Vout = Vin

So,
Vout(p-p) = 10 V

Maximum input:
Vin(max) = 5 V

Since Vcc = 13 V, the op-amp can provide this output without clipping.
### Transient Analysis
<img width="1915" height="878" alt="image" src="https://github.com/user-attachments/assets/4e850f6f-d01b-4289-b9df-63ed2e8b13c0" />

### Observation from Graph

The graph shows two waveforms:

- Green waveform → Input voltage (Vin)
- Blue waveform → Output voltage (Vout)

---

### Input Signal

- Type: Sinusoidal wave  
- Amplitude: 5 V  
- Peak-to-peak voltage: 10 V  
- Frequency: 1 kHz  

Vin = 5 sin(2πft)

---

### Output Signal

- Output waveform is also sinusoidal  
- Amplitude: 5 V  
- Peak-to-peak voltage: 10 V  
- Frequency: Same as input (1 kHz)

Vout = Vin

---

### Key Observations

1. No Gain (Unity Gain)  
   Output amplitude = Input amplitude  
   Av = Vout / Vin = 1  

2. No Phase Shift  
   Input and output peaks occur at the same time  

3. Waveform Shape  
   Both are identical sine waves  
   No distortion observed  

4. No Clipping  
   Output remains within ±5 V  
   Supply voltage (±13 V) is sufficient  

---

### Interpretation
- The op-amp is operating in linear region  
- Negative feedback ensures Vout = Vin  
- Load (4.7 kΩ) does not affect the signal  

---
### AC Analysis
<img width="1919" height="882" alt="image" src="https://github.com/user-attachments/assets/7dd0c26b-c535-4613-affa-ac707745aa19" />

### Reason for Dip in Frequency Response

### Explanation

- The dip in the graph is due to non-ideal behavior of the op-amp model (uA741)
- Internal poles and zeros interact at certain frequencies
- This causes a temporary drop in gain (dip)

---

### Additional Reason

- Simulation is run over a very wide frequency range (up to THz)
- At very high frequencies, the model becomes non-physical
- This produces artifacts like dips in the graph
- The dip is not a practical behavior
- It occurs due to internal op-amp limitations and simulation effects
- It appears beyond the useful bandwidth of the op-amp
---

## Output Analysis
- Output waveform is identical to input waveform
- No phase shift or distortion
- Load does not affect the input signal
- Suitable for driving low-resistance loads

---

## Conclusion
The voltage follower provides unity gain and is mainly used as a buffer. It ensures proper signal transfer without loading effects due to its high input impedance and low output impedance.


# Circuit-2  Non-Inverting Amplifier

## Aim
To design and analyze a non-inverting amplifier using an operational amplifier and verify the gain.

---

## Introduction
A non-inverting amplifier is an op-amp configuration in which the input signal is applied to the non-inverting terminal (+). The output is in phase with the input and amplified by a fixed gain determined by external resistors.

This configuration is widely used in signal amplification because it provides high input impedance, stable gain, and no phase inversion.

---

## Theory
The gain of a non-inverting amplifier is given by:

Av = 1 + (Rf / R1)

Where:
- Rf = Feedback resistor  
- R1 = Resistor connected to ground  

Thus,
Vout = Av × Vin

### Characteristics:
- No phase inversion
- High input impedance
- Low output impedance
- Stable gain due to negative feedback

---

## Working Principle
- Input is applied to the non-inverting terminal (+)
- Output is fed back to inverting terminal (−) through Rf
- R1 connects inverting terminal to ground
- Due to negative feedback:
  V− ≈ V+ = Vin

Hence,
Vout = (1 + Rf/R1) × Vin

---

## Circuit Design
<img width="627" height="492" alt="image" src="https://github.com/user-attachments/assets/52e41770-1bf0-4818-a1f8-be09877d09ea" />


### Configuration:
- Vin → Non-inverting terminal (+)
- Rf → Between output and inverting terminal (−)
- R1 → Between inverting terminal and ground

---

## Design Calculation

Given:
Vin(p-p) = 10 V  
Vcc = 13 V  
Required gain Av = 11  
### DC Analysis
<img width="1449" height="688" alt="image" src="https://github.com/user-attachments/assets/9b2fe40e-a608-4034-87ac-ad3c527f1201" />

Using:
Av = 1 + (Rf / R1)

11 = 1 + (Rf / R1)  
Rf / R1 = 10  

Choose:
R1 = 1 kΩ  
Rf = 10 kΩ  

---
## Transient Analysis
<img width="1915" height="852" alt="image" src="https://github.com/user-attachments/assets/03642766-0efe-4fd1-b969-0aabe5f285da" />

## Output Calculation

Vin(max) = 5 V  
Vout = 11 × 5 = 55 V  
Since supply voltage is ±13 V:

- Output cannot reach 55 V  
- Output will saturate at ≈ ±12 V  
- Clipping occurs because the required output voltage exceeds the supply voltage
- This causes distortion in the output waveform
  
---

## Output Analysis

- Output is amplified version of input  
- No phase shift  
- Clipping occurs due to supply limitation  
- Distortion appears at peaks  

---

## Waveform Observation

- Input → sine wave (10 Vp-p)  
- Output → amplified sine wave  
- Output peaks are clipped at supply limits  

---

## Frequency Response
<img width="1916" height="826" alt="image" src="https://github.com/user-attachments/assets/76d95900-242a-44f7-a7e8-0b5b597dea07" />


## Observation

- At low frequency:
  Gain ≈ 20.8 dB (since Av = 11)
- Gain remains constant up to bandwidth
- After cut-off frequency:
  Gain decreases

---

## Key Points

- Gain in dB:
  Av(dB) = 20 log(11) ≈ 20.8 dB  
- Bandwidth limited by op-amp (≈ 1 MHz for 741)
- Roll-off:
  -20 dB/decade  
- Phase shifts at high frequency  

---

## Conclusion

- Non-inverting amplifier provides high gain without phase inversion  
- Gain depends on resistor ratio  
- Output is limited by supply voltage  
- At high frequencies, gain decreases due to op-amp limitations

## Interpretation and Result

## 1. Voltage Follower

### Interpretation
- Output waveform is identical to input waveform  
- No phase shift is observed  
- Gain is unity (Av = 1)  
- No distortion or clipping occurs  
- High input impedance prevents loading effect  

### Result
The voltage follower works correctly as a buffer circuit, providing unity gain and maintaining signal integrity without distortion.

---

## 2. Non-Inverting Amplifier

### Interpretation
- Output waveform is amplified version of input  
- Output is in phase with input  
- Gain is high (Av = 11)  
- Output waveform shows clipping at peaks  
- Clipping occurs due to limited supply voltage  

### Result
The non-inverting amplifier successfully amplifies the input signal, but distortion occurs because the output exceeds the supply limits, resulting in saturation.
  
