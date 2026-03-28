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

First, calculate your Overdrive Voltage ($V_{OV}$):

$$
V_{OV} = V_{GS} - V_{TH} = 0.7V - 0.36 =**0.48mV**
$$

The absolute maximum limit before the circuit behaves entirely linearly  is:

$$
|v_{id}| \leq \sqrt{2} V_{OV}
$$

$$- \sqrt{2} V_{OV} \leq v_{id} \leq \sqrt{2} V_{OV}$$

$$ -0.48 \leq v_{id} \leq 0.48$$




 

  
  
  

  

  
  
