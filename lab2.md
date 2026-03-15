# LIC-lab2
# Experiment 2: CS amplifier with different configurations
# Experiment 2A: CS Amplifier with Resistor Load

# 1. Aim:
Design CS amplifier with PMOS active load configuration in tsmc180nmtech.lib in LTSPICE.

Given: VDD = 2V, Power <= 1.5mW, CL = 1pF, L = 180nm, Vin = 10mV, f = 1kHz

# 2. Theory:
**Circuit Topology Identification:**


* The NMOS transistor (M1) is the primary amplifying device. The input signal (VIN) is applied to its gate, and the output (vout) is taken from its drain, making this a Common-Source configuration.

* Active Load (M2): The PMOS transistor (M2) replaces a traditional passive drain resistor. Its gate is tied to a constant DC voltage (1.36V from V4), and its source is tied to $V_{DD}$ (2V from V1). This biases M2 to act as a constant current source. Using an active load provides a much higher small-signal output resistance, which significantly increases the theoretical voltage gain of the amplifier stage compared to using a standard resistor. * Source Degeneration (R1): The $1\text{k}\Omega$ resistor connected to the source of M1 provides local negative feedback (source degeneration).

**Effects:**

* Gain Stability: The voltage gain becomes less dependent on the highly variable transconductance ($g_m$) of the transistor and more dependent on the stable passive resistor values.
* Linearity: The negative feedback reduces nonlinear distortion, allowing the amplifier to handle larger input voltage swings without clipping.
* Increased Output Resistance: The resistance looking into the drain of M1 increases.


# 3. Circuit Diagram:
<img width="1116" height="545" alt="image" src="https://github.com/user-attachments/assets/f38d06a0-d4f7-40a1-881d-3eb3e55bf039" />

# 4. Design Calculation:
Given Specifications:

| **Parameter**               | **Symbol** | **Value**     | **Unit** |
| --------------------------- | ---------- | ------------- | -------- |
| Supply Voltage              | VDD        | 2             | V        |
| Overdrive Voltage           | VOV        | 0.25          | V        |
| Load Capacitance            | CL         | 1             | pF       |
| Channel Length (NMOS, PMOS) | Ln = Lp    | 180           | nm       |
| Maximum Power               | P ≤        | 1.5           | mW       |
| Relative Permittivity       | εr         | 3.9           | —        |
| Permittivity of Free Space  | ε₀         | 8.854 × 10⁻¹² | F/m      |
| Oxide Thickness             | tox        | 4.1 × 10⁻⁹    | m        |
| Electron Mobility           | μn         | 273.809       | cm²/V·s  |
| Hole Mobility               | μp         | 115.689       | cm²/V·s  |
# CMOS Amplifier Design (TSMC 0.18µm) – Calculation

- Assumed Drain Current:  
  ID = 200 µA


## For NMOS Design (M1):

## Gate Source Voltage

VGS = Vthn + Vov

VGS = 0.36 + 0.25

VGS = **0.61 V**

---

## Source Resistor

Assume voltage across source resistor:

VRS = 0.2 V

Using Ohm's law

ID × RS = VRS

200 × 10⁻⁶ × RS = 0.2

RS = **1 kΩ**

---

## Output Bias Voltage

Vout ≈ VDD/2 + 0.2

Vout = 2/2 + 0.2

Vout = **1.2 V**

---

## Width Calculation

MOSFET current equation

ID = (1/2) μnCox (W/L) (VGS − VT)²

Given

kn = μnCox = 230 × 10⁻⁶  
L = 180 nm  

Substitute values

200 × 10⁻⁶ = 1/2 × (230 × 10⁻⁶) × (W / 180 × 10⁻⁹) × (0.25)²

Solving

W ≈ **5 µm**

Thus

L = 0.18 µm  
W = 5 µm

---

## For Bias Voltage for M3

Gate voltage for M3:

VB1 = VGS + IDRS

VB1 = 0.61 + (200 × 10⁻⁶ × 1000)

VB1 = 0.61 + 0.2

VB1 = **0.81 V**

---

## PMOS Design (M2)

PMOS overdrive condition

VSG − |Vthp| = Vov

VSG = Vov + |Vthp|

VSG = 0.25 + 0.39

VSG = **0.64 V**

---

## Gate Bias Voltage

VB2 = VDD − VSG

VB2 = 2 − 0.64

VB2 = **1.36 V**

## PMOS Width Calculation
 Wp = (2 ID L) / (μp Cox (VOV)²)

Wp = 11.82 µm

---

## Summary of Design Parameters:

| Parameter | Value |
|-----------|-------|
| VDD | 2 V |
| ID | 200 µA |
| Vov | 0.25 V |
| RS | 1 kΩ |
| VGS (M1) | 0.61 V |
| VB1 | 0.81 V |
| VB2 | 1.36 V |
| NMOS W/L | 5 µm / 0.18 µm |
| PMOS W/L | 11.82 µm |

---

# 5. Simulation Setup (LTSpice)


# DC Analysis:
for Wn = 5 µm and Wp = 11.82 µm
<img width="846" height="520" alt="image" src="https://github.com/user-attachments/assets/aa55a6aa-fcce-4ae8-87d3-19e345778e42" />

After altering Width of mosfet to set operating point 
for Wn = 24.8 µm and Wp = 35.7 µm we get:

<img width="847" height="587" alt="image" src="https://github.com/user-attachments/assets/d49945e6-006e-4efc-802d-ba8e4f586818" />

1. Analysis of M1 (NMOS):

   - VGS = VG − VS
    VGS = 0.81 − 0.200035
    VGS = 0.609965 V
   - VDS = VD − VS
VDS = 1.22261 − 0.200035
VDS = 1.022575 V

Condition VDS ≥ VGS − Vthn is satisfied therefore mosfet is working in saturation region.

2. for M2(PMOS):
   VSG = VS − VG
VSG = 2.0 − 1.36
VSG = 0.64 V

VSD = VS − VD
VSD = 2.0 − 1.22261
VSD = 0.77739 V

Condition VSD ≥ VSG − |Vthp| is satisfied therefore mosfet is working in saturation region. 



# 7. DC Sweep Analysis:
<img width="1918" height="417" alt="image" src="https://github.com/user-attachments/assets/20f62c91-3ae8-450d-abb5-5525369a5457" />

# 8. Transient Analysis:

<img width="1918" height="920" alt="image" src="https://github.com/user-attachments/assets/3c199bf9-13e7-4c1b-87a9-3e5ede56710a" />

We can observe the 180 degree phase shift and the amplification of the output signal.

Peak to peak value of input voltage is : Vin(p-p) = 20mV 

Peak to peak value of output voltage is

Vout (max) = 1.34 V

Vout (min) =  1.09 V

Thus, Vout (p-p) = 0.25V

Av = Vout(p-p) / Vin(p-p)=12.5v/v

Av (in dB)=20*log(Av)=21.9dB


# 6. AC Analysis:

<img width="1915" height="913" alt="image" src="https://github.com/user-attachments/assets/c7fcc3ce-25ed-453d-992c-d823eaa59106" />

**midband gain=22.17dB**

**Bandwidth (frequency)=182.51602MHz**



# 7. Inference:









