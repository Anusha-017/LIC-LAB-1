# LIC-LAB-1
# Experiment 1: CS Amplifier Characterization in LTspice (180nm Technology)
## Aim:
Design cs ampifier using nmosfet in tsmc 180nm using vdd=2V , P<=1.5mW,capacitor = 1.5pF
## Theory:
A Common-Source (CS) amplifier is a popular transistor amplifier configuration where the input is applied to the gate and the output is taken from the drain, with the source serving as the common terminal. It provides voltage amplification by modulating the drain current in response to changes in the gate-source voltage. The output is 180° out of phase with the input, and the amplifier has high input and output impedance.For a Common-Source (CS) amplifier to work correctly, the conditions are ,V GS≥V th(to turn the transistor on),V DS>V GS −V th(to keep the transistor in saturation),The input signal vin should be small for small-signal operation,Proper biasing and selection of 𝑅Dare needed for stable operation and adequate voltage gain.

In saturation region the current formula is given by ID=1/2knVov
## Calculation:
1)Assuming ID =200µA which satisfy P<=1.5mW  (P=V*I ; 2×200×10^−6 ; 400µW<=1.5mW)

2)We know VDD-ID*RD=VDS

 2-200×10−6×RD=1

therefore RD=5K ohms

3)Kn′=μnCox

 Kn′= 230×10^−6 A/V^2

 4)VGS​=VG​−VS​=0.9−0=0.9V
  
  ID​=​K′W/L​(Vov​)^2

  W=1.07×10−6m
## Circuit 1: CS Amplifier with Resistor Load:
<img width="463" height="428" alt="Screenshot 2026-02-22 230401" src="https://github.com/user-attachments/assets/9a4aae73-e33b-4ab1-82fb-21addbca8119" />

## DC analysis:
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
## Transfer Analysis
<img width="1919" height="435" alt="Screenshot 2026-02-23 000216" src="https://github.com/user-attachments/assets/98bba263-ed62-4b2e-99ab-3ba6719c5cc8" />
# Common-Source NMOS Amplifier: DC Voltage Transfer Characteristic (VTC)

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
<img width="1919" height="870" alt="Screenshot 2026-02-23 002154" src="https://github.com/user-attachments/assets/4d4f8c1e-9ece-4abc-b77f-601823d1241c" />
From the graph we can calculate the gain of the circuit.

* **Av​**=ΔVin/​ΔVout
  
   Av=0.057/0.0186=3.06
* **Gain(dB)** = 20log10(Av)=9.714dB​​​
* **gm= 2Id / Vov=7.49×10^−4 S**
* **Av=gm×RD**

   Av=7.49×10^−4×5×10^3=3.74
* **Gain(dB)** = 20log10(Av)=11.36
* ## AC Analysis(without capacitor):
  <img width="1918" height="423" alt="image" src="https://github.com/user-attachments/assets/ad31a155-1f2c-4934-a000-fd3221276fd3" />
* **Av=9.4-3=6.4dB**
* Cutoff frequency=42.33GHz
* Bandwidth=42.33GHz
* ## AC Analysis(with capacitor):
 <img width="1912" height="416" alt="Screenshot 2026-02-22 233258" src="https://github.com/user-attachments/assets/f9cef3cf-13cb-4645-aad1-214cbe5786af" />
 
 * **C=1.5pF**
   
 *  Av=9.4-3=6.4dB
   
 *  Bnadwidth=24.27MHz
 



  

   ​​​

 

 










  
  
