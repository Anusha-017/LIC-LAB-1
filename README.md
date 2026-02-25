# LIC-LAB-1
# Experiment 1: CS Amplifier Characterization in LTspice (180nm Technology)
## Aim:
Design cs ampifier using nmosfet in tsmc 180nm using vdd=2V , P<=1.5mW,capacitor = 1.5pF
## Theory:
A Common-Source (CS) amplifier is a popular transistor amplifier configuration where the input is applied to the gate and the output is taken from the drain, with the source serving as the common terminal. It provides voltage amplification by modulating the drain current in response to changes in the gate-source voltage. The output is 180° out of phase with the input, and the amplifier has high input and output impedance.For a Common-Source (CS) amplifier to work correctly, the conditions are ,VGS≥Vth(to turn the transistor on),VDS>VGS −Vth(to keep the transistor in saturation),The input signal vin should be small for small-signal operation,Proper biasing and selection of 𝑅Dare needed for stable operation and adequate voltage gain.

In saturation region the current formula is given by ID=1/2knVov
## Procedure :

Step 1: Open LTspice and create a New schematic .Save the schematic with an appropriate name in the same folder where tsmc file is donwloaded.

Step 2:  Place the following components in the schematic-MOSFET (CMOSN or NMOS 180nm technology model)Resistor (R1 = 5kΩ)Voltage sources (V1 for DC supply, V2 for AC input signal)Ground connection (every circuit must have a ground reference).

Step 3: Set Component values DC supply (V1) = 2V (connect to drain through R1).AC input source V2 = SINE(0.9 10m 1k) (0.9V DC bias, 10mV AC signal, 1kHz frequency).Resistor (R1) = 5kΩ (between V1 and drain). MOSFET (M1) = 180nm NMOS model (drain connected to R1, source connected to ground, gate connected to V2).
Import MOSFET s(CMOS) datsheet which contains threshold and other specifications of mosfet 

Step 4: Configure simulation click on simulation then edit Simulation Cmd and enter the following:
 
DC Analysis:  .op to find DC operating point.
AC Analysis: .ac dec 10 0.1 100G to analyze gain and frequency response.
Transient Analysis: .tran 5m to observe the output waveform over time. Place these commands in the schematic.

Step 5: Run Simulation Click Run.View results in waveform viewer. Observing DC bias values, gain vs frequency response, and time-domain output waveform.

Step 6: Interpret The results for DC analysis, check VGS, VDS, and ID to confirm the MOSFET is operating. For AC analysis, check the gain plot and bandwidth.Respectively for transient analysis, observe the shape of the output waveform and check that amplification took place.
## Calculation:
1)Assuming ID =200µA which satisfy P<=1.5mW  (P=V*I ; 2×200×10^−6 ; 400µW<=1.5mW)

2)We know VDD-ID*RD=VDS

 2-200×10−6×RD=1

therefore RD=5K ohms

3)Kn′=μnCox

 Kn′= 230×10^−6 A/V^2

 4)VGS​=VG​−VS​=0.9−0=0.9V
  
  ID​=​Kn′*W/L​(Vov​)^2

  W=1.07×10−6m
## Circuit 1: CS Amplifier with Resistor Load:
<img width="463" height="428" alt="Screenshot 2026-02-22 230401" src="https://github.com/user-attachments/assets/9a4aae73-e33b-4ab1-82fb-21addbca8119" />

## DC analysis:
DC analysis means to find the operational point (bias point) MOSFET by calculating some different DC voltages and currents at various nodes of the circuit. For a common source amplifier, we should find the drain current (ID), gate-source voltage (VGS), and check whether the MOSFET is working in cut-off, triode, or saturation regions. It is important to perform the DC analysis since this sets the amplifier for the correct operational bias state before applying an AC signal.

<img width="627" height="327" alt="Screenshot 2026-02-22 233412" src="https://github.com/user-attachments/assets/47f261d8-837e-45f5-bbc2-20619c794113" />

From this simulation Vout=1.23,Vin=0.9v and Id=153µA
the load line equation is given by Vout=VDD-Id*RD. The calculated value does not match with simulated one so we will change the width to maintain the length at 180nm and obtain desired current value
| Length (nm) | Width (µm) | Id (µA) |
|-------------|------------|---------|
| 180        | 1.07       | 153      |
| 180        | 1.17       | 164.6   |
| 180        | 1.27       | 175.3   |
| 180        | 1.37      | 185.9   |
| 180        | 1.47      | 196.3   |
| 180        | 1.51       | 200   |

To check the mosfet is in saturation region
Vds=Vd-Vs ;1-0=1V

since Vds>Vov

It is in saturation region.The Q point is 1V,200µA
## Transfer Analysis:
Transfer characteristics depict how the drain current (Id) varies with the gate-to-source voltage (Vgs).It's ltspice command is ".dc V2 0 2"
Common-Source NMOS Amplifier: DC Voltage Transfer Characteristic (VTC):

<img width="1919" height="435" alt="Screenshot 2026-02-23 000216" src="https://github.com/user-attachments/assets/98bba263-ed62-4b2e-99ab-3ba6719c5cc8" />


## 1. Cutoff Region ($V_{in} < V_{th}$)

* **On the graph:** The flat horizontal line at the top left, where $V_{in}$ is between **0V** and approximately **0.4V**. 
* **Circuit behavior:** The input gate voltage is below the transistor's threshold voltage ($V_{th}$). The NMOS is completely turned **OFF**. Because no drain current ($I_D$) is flowing through the **5kΩ** resistor ($R_1$), there is no voltage drop across it. 
* **Equation:** $$V_{out} = V_{DD} - (I_D \cdot R_1)$$
  Since $I_D = 0$, $V_{out} = V_{DD} =$ **2.0V**.

## 2. Saturation Region ($V_{in} > V_{th}$ and $V_{out} > V_{in} - V_{th}$)

* **On the graph:** The steep, downward-sloping section in the middle, roughly between $V_{in} =$ **0.4V** and **1.0V**.
* **Circuit behavior:** As $V_{in}$ exceeds the threshold voltage, the NMOS turns **ON** and enters saturation. It begins to conduct current ($I_D$), which increases quadratically with $V_{in}$. As current flows through $R_1$, the voltage drop across the resistor increases, causing $V_{out}$ at the drain to drop rapidly. 
* **Significance:** This steep region is where the circuit operates as an amplifier. A small change in the input voltage ($V_{in}$) results in a large, inverted change in the output voltage ($V_{out}$). The slope of this line represents the voltage gain of the amplifier.

## 3. Triode / Linear Region ($V_{in} > V_{th}$ and $V_{out} < V_{in} - V_{th}$)

* **On the graph:** The flattened-out section on the bottom right, starting around $V_{in} =$ **1.2V** and extending to **2.0V**.
* **Circuit behavior:** As $V_{in}$ continues to increase, $V_{out}$ drops so low that the transistor leaves saturation and enters the triode region. Here, the MOSFET acts like a voltage-controlled resistor. The curve flattens out because the transistor's "on-resistance" is very low, pulling $V_{out}$ close to ground (**0V**), but it doesn't reach a perfect zero due to that small residual resistance.
## Transient Analysis:
Input voltage waveform:

<img width="1917" height="911" alt="vin lab1" src="https://github.com/user-attachments/assets/b5cd4e5f-6d30-4642-8674-a98b952c56c4" />

Output waveform:


<img width="1919" height="891" alt="Screenshot 2026-02-25 081308" src="https://github.com/user-attachments/assets/471b2e36-7272-46af-a24d-6484a922dc0b" />

Input and output waveform:

<img width="1919" height="870" alt="Screenshot 2026-02-23 002154" src="https://github.com/user-attachments/assets/4d4f8c1e-9ece-4abc-b77f-601823d1241c" />

* **Graph Interpretation**:
* 
* Amplification (Voltage Gain):The voltage gain ($A_v$) is the ratio of output AC amplitude to input AC amplitude.
* Phase Shift (Signal Inversion):This represents a 180-degree phase shift. This happens because as the input gate voltage increases, the transistor turns "on" , drawing more drain current. This increased current causes a larger voltage drop across the 5kΩ drain resistor (R1), which in turn lowers the voltage at the drain node (Vout).
  
* From the graph we can calculate the gain of the circuit.

* **Av​**=ΔVin/​ΔVout
  
   Av=56.7×10^-3/19.13×10^-3=3.06v/v
* **Gain(dB)** = 20log10(Av)=9.71dB​​​
* We know that **gm= 2Id / Vov=7.49×10^−4 S**
* **Av=gm×RD**

   Av=7.49×10^−4×5×10^3=3.74v/v
* **Gain(dB)** = 20log10(Av)=11.36
* ## AC Analysis(without capacitor):
  
AC analysis depicts how the amplifier's gain (𝐴𝑣) changes with frequency as it is a critical way of studying the frequency response of the amplifier.We can also find the bandwidth.the MOSFET behavior will have to be linearized around its bias point. AC analysis is done in LTspice using the .ac dec 10 0.1 100G command
Ac gain can be calulated using equation Av = -gm *Rd

  <img width="1918" height="423" alt="image" src="https://github.com/user-attachments/assets/ad31a155-1f2c-4934-a000-fd3221276fd3" />
  
* **Av=9.4-3=6.4dB**
 
* Cutoff frequency=42.33GHz
  
* Bandwidth=42.33GHz
  
  ## AC Analysis(with capacitor):


<img width="466" height="445" alt="Screenshot 2026-02-22 232608" src="https://github.com/user-attachments/assets/fed3440a-27db-4fff-bf6c-83d990d763ef" />


Output Graph:

 <img width="1912" height="416" alt="Screenshot 2026-02-22 233258" src="https://github.com/user-attachments/assets/f9cef3cf-13cb-4645-aad1-214cbe5786af" />
 
 * **C=1.5pF**
   
 *  Av=9.4-3=6.4dB
   
 *  Bandwidth=24.27MHz
   

   ### Inference: 

1.DC Analysis- Determines the quiescent operating point(Q point) and ensures the NMOS operates in the saturation region for proper amplification.  


2.AC Analysis- it is observed that the load capacitance introduces a dominant pole at the output, limiting the high-frequency response of the amplifier.

Hence, the CS amplifier design meets the required specifications and demonstrates proper biasing, gain performance, and bandwidth characteristics


3.Transient Analysis-Validates the amplifier’s response to a time-varying signal. Confirms signal amplification and phase inversion, which is a characteristic of a common source amplifier.  


4.Frequency Response -
Bandwidth and Cutoff Frequency This is where the capacitor makes a difference:

Without Capacitor: The bandwidth is extremely high at $42.33\text{ GHz}$. The amplifier can sustain its gain at very high frequencies because it isn't fighting against a heavy capacitive load.

With Capacitor: The bandwidth drops significantly to $24.27\text{ MHz}$.The $1.5\text{ pF}$ capacitor, combined with the output resistance of the amplifier ($5\text{ k}\Omega$ resistor $R_1$), creates a low-pass filter effect. This combination forms a "dominant pole" that shunts high-frequency AC signals to ground much earlier than the intrinsic MOSFET would on its own.



 



  

   ​​​

 

 










  
  
