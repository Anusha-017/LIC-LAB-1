# LIC-lab2
# Experiment 2: CS amplifier with different configurations
# Experiment 2A: CS Amplifier with Resistor Load

# 1. Aim:
Design CS amplifier with PMOS active load configuration in tsmc180nmtech.lib in LTSPICE.

Given: VDD = 2V, Power <= 1.5mW, CL = 1pF, L = 180nm, Vin = 10mV, f = 1kHz

# 4. Theory:
**Circuit Topology Identification:**


* The NMOS transistor (M1) is the primary amplifying device. The input signal (VIN) is applied to its gate, and the output (vout) is taken from its drain, making this a Common-Source configuration.

* Active Load (M2): The PMOS transistor (M2) replaces a traditional passive drain resistor. Its gate is tied to a constant DC voltage (1.36V from V4), and its source is tied to $V_{DD}$ (2V from V1). This biases M2 to act as a constant current source. Using an active load provides a much higher small-signal output resistance, which significantly increases the theoretical voltage gain of the amplifier stage compared to using a standard resistor. * Source Degeneration (R1): The $1\text{k}\Omega$ resistor connected to the source of M1 provides local negative feedback (source degeneration).

**Effects:**

* Gain Stability: The voltage gain becomes less dependent on the highly variable transconductance ($g_m$) of the transistor and more dependent on the stable passive resistor values.
* Linearity: The negative feedback reduces nonlinear distortion, allowing the amplifier to handle larger input voltage swings without clipping.
* Increased Output Resistance: The resistance looking into the drain of M1 increases.


# 3. Circuit Diagram:
<img width="1116" height="545" alt="image" src="https://github.com/user-attachments/assets/f38d06a0-d4f7-40a1-881d-3eb3e55bf039" />

# 5. Design Calculation:
Given Specifications:

* VDD = 2 V

* VOV = 0.25 V

* CL = 1 pF

* Ln = Lp = 180 nm

* P<= 1.5mW

* εr = 3.9

* ε0 = 8.854 × 10⁻¹² F/m

* tox = 4.1 × 10⁻⁹ m

* μn = 273.809 cm²/Vs

* μp = 115.689 cm²/Vs

1)Power constraint:
  
  Assuming ID =200µA which satisfy P<=1.5mW (P=V*I ; 2×200×10^−6 ; 400µW<=1.5mW)

2)Output Voltage :

 Vout = VDD/2 + VRS

 Vout = 1 + 0.2 = 1.2 V

3)NMOS Width Calculation:

 Drain current equation:  ID = (1/2) kn' (W/L) (VOV)^2

Where

kn' = μn Cox

Cox = εox / tox

kn' = 2.306 × 10⁻⁴

Now solving for W:

W = 5 µm
4)PMOS Width Calculation
 Wp = (2 ID L) / (μp Cox (VOV)²)

Wp = 11.82 µm

# DC Analysis:
for Wn = 5 µm and Wp = 11.82 µm
<img width="846" height="520" alt="image" src="https://github.com/user-attachments/assets/aa55a6aa-fcce-4ae8-87d3-19e345778e42" />


for Wn = 24.8 µm and Wp = 35.7 µm
<img width="847" height="587" alt="image" src="https://github.com/user-attachments/assets/d49945e6-006e-4efc-802d-ba8e4f586818" />

# 7. DC Sweep Analysis:
<img width="1918" height="417" alt="image" src="https://github.com/user-attachments/assets/20f62c91-3ae8-450d-abb5-5525369a5457" />

# 8. Transient Analysis:

<img width="1918" height="920" alt="image" src="https://github.com/user-attachments/assets/3c199bf9-13e7-4c1b-87a9-3e5ede56710a" />




# 9. AC Analysis:
<img width="1918" height="877" alt="image" src="https://github.com/user-attachments/assets/9f9f8db5-ce11-4691-87d8-0647bce87cd2" />



# 10. Inference:









