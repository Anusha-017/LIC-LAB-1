# Differential Amplifier Report and Analysis
## **Introduction**

A **Differential Amplifier** is a fundamental building block in analog circuit design, most notably serving as the input stage for operational amplifiers (Op-Amps). Its primary function is to amplify the difference between two input signals while rejecting any signals that are common to both.

This characteristic makes it incredibly effective in environments with high electromagnetic interference, as noise typically affects both input lines equally (common-mode) and is therefore cancelled out. 

Differential amplifiers provide high common-mode rejection, making them ideal for applications where noise and interference must be minimized. These amplifiers are widely used in communication systems, medical instrumentation, and control systems.  

The working principle of a differential amplifier is based on transistor pair operation, where two identical transistors share a common bias current source. When a differential input is applied, the current is steered between the two transistors based on the voltage difference, allowing for signal amplification.  

Mathematically, the differential mode gain (Ad) and common mode gain (Ac) are given by:  
```
Ad = RD / re
Ac = (gm * RD) / (2 + gm * re)
```
where:  
- **RD** is the drain resistor  
- **re** is the small-signal emitter resistance  
- **gm** is the transconductance

A perfect differential amplifier ideally has an infinite common-mode rejection ratio (CMRR), but practical limitations lead to finite CMRR. 

* **Differential-Mode Gain ($A_d$):** This occurs when the two input signals are different. The amplifier responds to the voltage difference $(V_{in1} - V_{in2})$.

* **Common-Mode Gain ($A_c$):** This occurs when the same signal is applied to both inputs. In an ideal differential amplifier, the output should be zero, meaning $A_c = 0$.

* **Common-Mode Rejection Ratio (CMRR):** This is a key figure of merit that measures the amplifier's ability to reject common-mode signals. It is defined as:

$$CMRR = \left| \frac{A_d}{A_c} \right|$$

Higher CMRR values indicate better performance, typically expressed in decibels (dB).

### **Key Parameters:** 
- Input Common-Mode Range : The voltage range over which the differential pair amplifier circuit functions properly.
- Differential Gain : Determines the amplification of the differential signal.
- Input & Output Swing: Maximum and minimum voltages the amplifier can handle without distortion.
- Common-Mode Rejection Ratio (CMRR): A high CMRR ensures better noise rejection.
  
## **Problem Statement**

To design and analysis of the MOS differenrial amplifier circuit for the following soecification  :
- **Vdd** = 0.9V
- **L** = 180nm
- **Power** <= 1.5mW
- **Vincm** = 0V
- **Vocm** = 0V
- **Vp** = -0.7V
- **VSS** = -0.9V

  ## **Circuit 1: Differential Amplifier with a Resistive Load:**
  
 ### Circuit diagram :
 <img width="1377" height="710" alt="image" src="https://github.com/user-attachments/assets/e251d088-58b4-4ae4-81f3-e45e2b9fc053" />

 ### Design Calculations:
### Step 1: DC Analysis & Fixing the Operating Point

#### 1. Calculate the Tail Current ($I_{SS}$):

Using the power specification to find the maximum allowed current.

$$P = (V_{DD} - V_{SS}) \times I_{SS}$$

$$1.5mW = (0.9V - (-0.9V)) \times I_{SS}$$

$$I_{SS} = \frac{1.5mW}{1.8V}$$

$$**I_{SS} = 0.833mA**$$

#### 2. Calculate the Load Resistor ($R_D$):
Since the output common-mode voltage is $0V$, and the current splits equally between the two branches at equilibrium ($I_{D1} = I_{D2} = I_{SS}/2$), use the voltage drop equation:

$$V_{oCM} = V_{DD} - (I_{D1} \times R_D)$$

$$0V = 0.9V - \left( \frac{I_{SS}}{2} \right) \times R_D$$

$$RD=2.16KΩ$$


#### 3. Determine Transistor Aspect Ratio ($W/L$):
 $V_{inCM}$ and $V_p$, which allows you to find the Gate-Source Voltage ($V_{GS}$) for $M_1$ and $M_2$:

$$V_{GS} = V_{inCM} - V_p = 0V - (-0.7V) = 0.7V$$

Now, use the standard saturation region current equation (assuming your technology parameters like $\mu_n C_{ox}$ and $V_{TH}$ are known from your lab setup):

$$I_{D1} = \frac{1}{2} \mu_n C_{ox} \left( \frac{W}{L} \right) (V_{GS} - V_{TH})^2$$

On substituting  $I_{D1} = I_{SS}/2=0.4165mA$, $V_{GS} = 0.7V$, and $L = 360nm$ ,We get $W=11.23µm$.

### **DC Analysis**

<img width="1731" height="772" alt="image" src="https://github.com/user-attachments/assets/6e92e5d7-a5ed-425b-bb44-6f9ff7dde32e" />

 W1=W2 = 19.9 um
 
Total current I(V4) that is Iss = 0.833mA

Id1 = Id2 = 0.4165 mA

Q-point for M1 and M2 (NMOS) matches theoretical values:

VP = -0.7V, Id = Iss/2 = 0.4165mA

### Input Common Mode Range (ICMR)

#### Maximum Input Common-Mode ($V_{inCM(max)}$):

This is the highest input voltage before the input transistors ($M_1$ and $M_2$) get pushed out of the saturation region and into the triode region. This occurs when the gate voltage exceeds the drain voltage by more than $V_{TH}$.

$$V_{inCM(max)} = V_{D} + V_{TH}$$

Since your $V_{D}$ is $0V$:

$$V_{inCM(max)} = V_{TH}$$

$$V_{inCM(max)} = 0.361V$$

#### Minimum Input Common-Mode ($V_{inCM(min)}$):

This is the lowest input voltage before the tail current source runs out of "headroom" to operate. Because you are using an ideal current source in this specific schematic ($I_1$), it can theoretically operate all the way down to $V_{SS}$.

$$V_{inCM(min)} = V_{SS} + V_{GS}$$

$$V_{inCM(min)} = -0.9V + 0.7V = -0.2V$$

### Output Common Mode Range:

#### Maximum Output Common-Mode ($V_{oCM(max)}$):

This occurs if the transistors are completely off (zero current flowing through $R_D$). There is no voltage drop across the resistors.

$$V_{oCM(max)} = V_{DD} = 0.9V$$

#### Minimum Output Common-Mode ($V_{oCM(min)}$):

This is the lowest the output can swing before forcing $M_1$ and $M_2$ into the triode region (assuming $V_{inCM}$ is fixed at $0V$).

$$V_{oCM(min)} = V_{DD} - (Iss/2)*R_{D} = $$

$$0.9V-1.799V$$

$$-0.899V$$

### Linear Differential Input Range ($v_{id}$)

A differential amplifier only behaves linearly for small input signals. If the differential input ($v_{id}$) gets too large, all the current steers to one transistor, causing the output to clip.

Overdrive Voltage ($V_{OV}$):

$$
V_{OV} = V_{GS} - V_{TH} = 0.7V - 0.36 =**0.48mV**
$$

The absolute maximum limit before the circuit behaves entirely linearly  is:

$$
|v_{id}| \leq \sqrt{2} V_{OV}
$$

$$- \sqrt{2} V_{OV} \leq v_{id} \leq \sqrt{2} V_{OV}$$

$$ -0.48 \leq v_{id} \leq 0.48$$

## Transient Analysis:

### Case 1: Linear Region vin=100mV

<img width="765" height="403" alt="image" src="https://github.com/user-attachments/assets/03ca6e0b-4345-46c7-95c1-f045859998c6" />


<img width="1917" height="468" alt="image" src="https://github.com/user-attachments/assets/dad295e8-546a-487e-8ca7-5abb022e2156" />


<img width="1918" height="925" alt="final tran " src="https://github.com/user-attachments/assets/089fd711-85a4-49e6-acf8-354edc11d304" />


### Key Observations:

* **Linear Amplification:** The output waveforms, $V(out1)$ in green and $V(out2)$ in red, are clean, smooth sinusoids. There is no clipping or flattening at the peaks or troughs. This confirms that your $100mV$ input signal satisfies the small-signal condition $v_{id} < \sqrt{2}V_{OV}$, keeping both transistors ($M_1$ and $M_2$) entirely in the saturation region throughout the entire cycle.

* **Voltage Gain:** The blue trace (input) has a peak amplitude of exactly $200mV$. The resulting output traces have a peak to peak is  $1.03V$. This means the

circuit voltage gain of  

$$Vout(peak-peak)/Vin(peak-peak)$$

$$(1.03V / 200mV)$$

$$**5.15v/v**$$
  
$$ Gain in dB =20*log(5.15)$$

$$=14.06dB$$

* **Differential Phase Shift:** $V(out1)$ and $V(out2)$ are exactly $180^{\circ}$ out of phase with each other. As one transistor conducts more current and pulls its drain voltage down, the other conducts less, allowing its drain voltage to rise. This is the defining characteristic of a balanced differential pair.

* **Maintained Common-Mode:** Both output waves are perfectly centered exactly on the $0V$ axis. This verifies that DC operating point of $V_{oCM} = 0V$ holds steady even when a dynamic AC signal is applied.

#### Case 2: Non-Linear Region vin=600mV

**Output waveform:**

<img width="1912" height="422" alt="non linear tran" src="https://github.com/user-attachments/assets/b0d09eca-5dd2-49d9-8490-5339d5c60f02" />

### Key Observations: Non-Linear Behavior (Large Signal)

* **Severe Clipping (Limiting):** The output waveforms ($V(out1)$ in green and $V(out2)$ in blue) are no longer smooth sine waves. They have flattened tops and bottoms, closely resembling square waves. This indicates the amplifier is saturating and operating completely outside its linear amplification range.

* **Maximum Output Swing (High State):** When a transistor turns OFF, zero current flows through its $2.16k\Omega$ load resistor ($R_D$). Consequently, there is no voltage drop, and the output node is pulled all the way up to the positive supply rail, $V_{DD}$ (**$+0.9V$**).The green and blue traces flattening precisely at $+0.9V$.

* **Minimum Output Swing (Low State):** When a transistor is forced to carry the full tail current, the maximum possible voltage drop occurs across $R_D$ ($0.833mA \times 2.16k\Omega \approx 1.8V$). This pulls the output node down from $0.9V$ to $0.9V - 1.8V = -0.9V$.The negative supply rail, $V_{SS}$ (**$-0.9V$**), which is where the bottom of the waveforms flatten out.

* **Loss of Linear Gain:** In this state, the concept of small-signal voltage gain ($A_v$) is invalid. The circuit is highly distorted and is functioning more like a comparator or a voltage limiter rather than an amplifier.

### The graph shows currents across resisters:

<img width="1912" height="423" alt="image" src="https://github.com/user-attachments/assets/29cfb58e-1a61-418d-bc68-bd6e94893ecb" />

The input signal ($V(n002)$ in red) is very large ($|v_{id}| > \sqrt{2}V_{OV}$). Instead of sharing the tail current ($I_{SS}$), the differential pair acts like a switch. During the positive and negative peaks, one transistor completely turns OFF, forcing the other transistor to conduct the entire $0.833mA$ tail current.

## Theoretical Gain:

Differential Gain $Ad=gmRout$

### Calculation for gm value:
$$g_m = \frac{2I_D}{V_{OV}} = \frac{2I_D}{V_{GS} - V_{TH}}$$
$$g_m =\frac{2 \times 0.433 \times 10^{-3}}{0.7 - 0.34}$$
$$=2.405mS$$

Differential Gain $Ad=gmRout$

$$=2.405mS*2.16Kohms$$

$$=**5.196V/V**$$

- Gain (dB)= 20*log(5.19) = **14.31dB**

## AC Analysis:



<img width="1150" height="638" alt="image" src="https://github.com/user-attachments/assets/f7a0caeb-d6dc-4834-9d37-e8c5b638dded" />




<img width="1918" height="882" alt="image" src="https://github.com/user-attachments/assets/c480cfc7-2b3d-4e80-bdad-40c487e13c40" />



- ### Midband Gain= 16.08dB= 6.368 V/V
  

- ### -3dB Gain=13.25dB

<img width="1917" height="576" alt="image" src="https://github.com/user-attachments/assets/8653d767-d4a8-495a-90db-4a644d74d800" />


   * Lower cutoff frequency: fL = 0 Hz

   * Upper cutoff frequency: fH = 8.03 MHz

   * Bandwidth:
    $$BW = fH − fL$$

    $$BW = 8.03 MHz − 0$$
  
    BW = **8.03 MHz** 
- ### UGB:
 Unity Gain Bandwidth (UGB) is the frequency at which an operational amplifier's open-loop gain drops to 1 (0dB)
 
<img width="1918" height="857" alt="image" src="https://github.com/user-attachments/assets/f07f721c-a00f-4235-8140-1549cc3a475f" />

From AC analysis plot At frequency at 549.82901µdB ≈ 0dB = **51.19 MHz**


- ### Gain-Bandwidth Product (GBW):

  Multiply the linear mid-band gain by the $-3dB$ frequency.

* $$GBW = A_v \times f_{-3dB}$$

* $$GBW =  8.03 \times 4.597\text{ GHz} = 36.91 \text{ MHz}$$

## Inference
Circuit 1 demonstrates (NMOS Differential Amplifier with Resistive Load .The fundamental operation of the differential pair was successfully verified. The circuit effectively amplifies the difference between the two input signals ($v_{id}$). Conversely, when the exact same signal is applied to both inputs (a pure common-mode signal), the ideal tail current source forces the differential output to effectively zero, demonstrating the amplifier's ability to reject common-mode noise. 


  
  # Circuit 2: Differential Amplifier with diode-connected PMOS active load and an NMOS tail current source
  
## Theory

 1. Circuit Components & Structure

* **Differential Pair ($M_1, M_2$):** Two identical NMOS transistors that receive the input signals $V_{in1}$ and $V_{in2}$.
* **Active Loads ($M_4, M_5$):** Diode-connected PMOS transistors acting as resistive loads. Since they are diode-connected ($V_{GS} = V_{DS}$), they operate in the saturation region and provide a small-signal resistance of approximately $1/g_m$.
* **Current Source ($M_3$):** An NMOS transistor biased by $V_B$ to act as a constant tail current source ($I_{SS}$), ensuring the sum of currents through both branches remains constant.


---

2. Theory of Operation

The circuit operates by steering current between the two branches based on the voltage difference at the gates of $M_1$ and $M_2$.

### Common-Mode Behavior
If $V_{in1} = V_{in2}$, the current $I_{SS}$ splits equally:
$$I_{D1} = I_{D2} = \frac{I_{SS}}{2}$$
In this state, the output voltages $V_{out1}$ and $V_{out2}$ remain equal.

### Differential-Mode Behavior
If $V_{in1} > V_{in2}$, $M_1$ pulls more current than $M_2$. 
* This increase in current through $M_1$ causes a larger voltage drop across the load $M_4$, pulling $V_{out1}$ lower.
* Simultaneously, $V_{out2}$ rises.

### The "Tail" Node ($V_P$)
This node acts as a **"virtual ground"** for differential signals. This characteristic allows for the use of the **half-circuit lemma**, simplifying the analysis by focusing on just one-half of the symmetric circuit.


 ### Circuit Diagram:
 
<img width="928" height="831" alt="image" src="https://github.com/user-attachments/assets/4134cbc1-0e8e-4795-9e1b-0d1f471b4398" />

 ## Design Calculations:

#### 1. Tail Current ($I_{SS}$) Calculation

The power and supply voltages define the maximum allowed current for the entire circuit.

$$V_{Total} = V_{DD} - V_{SS} = 0.9V - (-0.9V) = 1.8V$$

$$P = V_{Total} \times I_{SS}$$

$$1.5mW = 1.8V \times I_{SS}$$

$$I_{SS} = 0.833mA$$

At DC equilibrium, this current splits equally between the two branches:

$$I_{D1} = I_{D2} = I_{D4} = I_{D5} = 0.4165mA$$

#### 2. Width Calculation: ($M_1$ and $M_2$)


The operating conditions for the input pair: 
* $V_{inCM} = 0V$
* $V_p = -0.7V$
* $V_{GS1,2} = V_{inCM} - V_p = 0.7V$


$$I_{D1} = \frac{1}{2} \mu_n C_{ox} \left( \frac{W}{L} \right) (V_{GS} - V_{TH})^2$$

On substituting  $I_{D1} = I_{SS}/2=0.4165mA$, $V_{GS} = 0.7V$, and $L = 360nm$ ,We get $W=11.23µm$.

#### 3. Width Calculation: ($M_4$ and $M_5$)
The operating conditions for pmos: 
* $V_{s} = VDD$
* $V_G = V_D = 0V$
* $V_{SG4,5} = V_{DD} - V_G = 0.9V$

$$I_{D1} = \frac{1}{2} \mu_n C_{ox} \left( \frac{W}{L} \right) (V_{GS} - V_{TH})^2$$

On substituting  $I_{D1} = I_{SS}/2=0.4165mA$, $V_{SG} = 0.9V$, and $L = 360nm$ ,We get $W=11.82µm$.


#### 3. Width Calculation: ($M_3$)
The operating conditions for M3: 
* $V_{D} = V_P = -0.7V$
* $V_S = -0.9V$
* $V_DS=-0.7-(0.9)=0.2V$
* $V_OV=V_GS-V_TH$
  $V_ov3 = V_B -(-0.9)-V_TH$
  
* For saturation $V_DS >V_OV$
  Assuming Vov=0.17V
  therefore $V_B=0.17-0.54$
  $=-0.37V$
    
## **DC Analysis**

<img width="745" height="863" alt="image" src="https://github.com/user-attachments/assets/8eec96ea-073b-4448-9a42-1115602f9a6f" />

#### Operating Regions:

To ensure the differential pair functions as an amplifier, we verify the saturation condition:
$V_{DS} > V_{GS} - V_{TH}$ (or $V_{DS} > V_{ov}$).

* **Input Pair ($M_1, M_2$):** * $V_{DS} = V_{out} - V_P = 0\text{V} - (-0.7\text{V}) = 0.7\text{V}$.
    * With $V_{GS} = 0.7\text{V}$, these devices stay in saturation.
* **Active Load ($M_4, M_5$):** * These are diode-connected (as seen in the schematic where Gates are tied to Drains). Diode-connected FETs are **always in saturation** (or cutoff) because $V_{DS} = V_{GS}$, satisfying $V_{DS} > V_{GS} - V_{TH}$.
* **Tail Current Source ($M_3$):** * $V_{DS} = V_P - V_{SS} = -0.7\text{V} - (-0.9\text{V}) = 0.2\text{V}$.
    * The bias voltage $V_4 = -0.37\text{V}$ results in $V_{GS} = -0.37 - (-0.9) = 0.53\text{V}$.
    * The simulation confirms $M_3$ is effectively sourcing the calculated $0.833\text{mA}$.
 
### Input Common Mode Range (ICMR)
* Minimum input voltage:

Condition $Vgs ≥ Vth$
   $Vgs = Vicm − Vs$

Vicm(min) = $Vs + Vth$

     $Vicm(min) =0.7+0.36 $
       
       $-0.34 V$

* Maximum input voltage:

Vicm(max) ≈ Vd + |Vtp|

$Vicm(max) = 0+0.39$
$=0.39 V$

#### **ICMR:**

$-0.34 V ≤ Vicm ≤ 0.39 V$

#### Output Common Mode Range (OCMR)
* Minimum output voltage

Vout(min) ≥ Vs + Vov

Vout(min) = -0.7+0.34
$=-0.36 V$

* Maximum output voltage

Vout(max) ≤ VDD − Vov

VDD = 0.9 V
Vov(p) = 0.25 V

Vout(max) = 0.9-0.25
$=0.65 V$

#### **OCMR:**

$-0.36 V ≤ Vout ≤ 0.65 V$

## Transient Analysis:

The linearity condition :

$$
|v_{id}| \leq \sqrt{2} V_{OV}
$$

$$- \sqrt{2} V_{OV} \leq v_{id} \leq \sqrt{2} V_{OV}$$

$$ -0.189 \leq v_{id} \leq 0.189$$


* linear operation :vin=10mV

<img width="1918" height="555" alt="image" src="https://github.com/user-attachments/assets/63a0a5d0-50be-44ee-a64d-eeed4001e54e" />

Observations:
* **Linear Amplification:** The output waveforms, $V(out1)$ in green and $V(out2)$ in red, are clean, smooth sinusoids. There is no clipping or flattening at the peaks or troughs. This confirms that $10mV$ input signal satisfies the small-signal condition $v_{id} < \sqrt{2}V_{OV}$, keeping both transistors ($M_1$ and $M_2$) entirely in the saturation region throughout the entire cycle.

## Simulated Gain:

<img width="1917" height="546" alt="image" src="https://github.com/user-attachments/assets/338ba029-11b9-4415-aa02-d9bf800ee747" />

 $$Gain=Vout(peak-peak)/vin(peak-peak)$$
 
$$38.20/20 =1.91V/V$$

$$Differential Gain (A_v,diff)	2 × 1.913= 3.826 V/V $$

$$Gain in dB =11.65dB$$

* non linear operation :vin=600mV

<img width="1916" height="466" alt="image" src="https://github.com/user-attachments/assets/1ceee866-2860-4cf5-8533-ed2432476e5a" />

Observations:

* **Severe Clipping (Limiting):** The output waveforms ($V(out1)$ in green and $V(out2)$ in blue) are no longer smooth sine waves. They have flattened tops and bottoms, closely resembling square waves. This indicates the amplifier is saturating and operating completely outside its linear amplification range.

* **Loss of Linear Gain:** In this state, the concept of small-signal voltage gain ($A_v$) is invalid. The circuit is highly distorted and is functioning more like a comparator or a voltage limiter rather than an amplifier.
## Theoretical Small-Signal Gain

### Transconductance

gₘ = 2I_D / V_OV  
gₘ = (2 × 0.4166 mA) / 0.340 V = 2.45 mS  

---

###  Output Resistance

r_o1 (NMOS M1):  
r_o1 = 1 / (λ_n × I_D)  
r_o1 = 1 / (0.1 × 0.4166 mA) = 24.0 kΩ  

r_o4 (PMOS M4):  
r_o4 = 1 / (λ_p × I_D)  
r_o4 = 1 / (0.1 × 0.4166 mA) = 24.0 kΩ  

R_out:  
R_out = r_o1 || r_o4  
R_out = (24.0 × 24.0) / (24.0 + 24.0) kΩ = 12.0 kΩ  

---

### Differential Voltage Gain

A_d = gₘ × R_out  
A_d = 2.45 × 10⁻³ × 12,000 = 29.4 V/V ≈ 29.4 dB

### AC Analysis:

<img width="1915" height="841" alt="image" src="https://github.com/user-attachments/assets/2babb1dd-ce6c-4a0b-a9fe-4272d0975483" />

ugb:
<img width="1918" height="661" alt="image" src="https://github.com/user-attachments/assets/29fe9457-d978-420d-a75e-4b448c9da79e" />




 

  
  
  

  

  
  
