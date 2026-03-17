# Experiment 2C – Common Source Amplifier with Diode-Connected NMOS Current Source and PMOS Active Load

# Circuit Digram :
<img width="885" height="621" alt="Image" src="https://github.com/user-attachments/assets/7e35739d-3ef4-4dcf-8cdc-452e369256a4" />

# Design Calculation:

Given Specifications:
### Design Parameters:

| Parameter | Symbol | Value |
|-----------|--------|-------|
| Supply Voltage | VDD | 2 V |
| Drain Current | ID | 200 µA |
| Overdrive Voltage | VOV | 0.25 V |
| Power Constraint | P | ≤ 1.5 mW |
| Relative Permittivity | εr | 3.9 |
| Permittivity of Free Space | ε0 | 8.854 × 10⁻¹² F/m |
| Oxide Thickness | tox | 4.1 × 10⁻⁹ m |
| Electron Mobility | μn | 273.809 cm²/Vs |
| Hole Mobility | μp | 115.689 cm²/Vs |

- M3 MOSFET(Always in saturation region):
  
 VGS3=VOV+VTH
 
   =0.25+0.36=0.61V
     
  VGS3=VG3-VS3
  
   =VG3=0.61V=VS1
      
- M1(nmos):
  
  VGS1=VOV+VTH
  
   =0.25+0.36=0.61V
  
  VGS1=VG1-VS1
  
   =VG1-0.61V
  
  VG1=1.22=**VIN**
  
- M2(PMOS Active load)
  
  VGS3=VOV+VTH

   0.25+0.39=0.64V
  
  VB1=VDD-VSG3
  
     =2-0.64=1.36V
  
- Width Calculation :
  
  Current equation is given as :
  
  ID = (1/2) kn' (W/L) (VOV)^2
  
  For M1 and M3 on substitution width comes to be 5 µm anD for M2 is  11.82 µm

# DC Operating Point:
To obtain desired operating point width of mosfet is varied 

### Transistor Dimensions

| Transistor | Type | Width (W) | Length (L) |
|-----------|------|-----------|-----------|
| M1 | NMOS | 14.3 µm | 0.18 µm |
| M2 | PMOS | 35 µm | 0.18 µm |
| M3 | NMOS | 14.3 µm | 0.18 µm |


<img width="851" height="486" alt="Image" src="https://github.com/user-attachments/assets/4424d991-990d-4942-bdcf-aa955b826268" />

# DC Sweep Analysis:  

<img width="1917" height="605" alt="Image" src="https://github.com/user-attachments/assets/00fc67b6-376b-44d1-98c5-3e2601e79467" />

# Transient Analysis:
<img width="1917" height="872" alt="Image" src="https://github.com/user-attachments/assets/0ac84d80-0c75-40c7-8cd4-8cb2de174067" />

<img width="1917" height="878" alt="Image" src="https://github.com/user-attachments/assets/3b4512e5-af0c-47b9-a002-6847755114f9" />

### Gain Calculation: 
Gain(Av)=vout(p-p)/vin(p-p)

       =355.506mV/19.709mV
       
        =18.03V/V
Gain (dB)=20*log(Av)

         = 25.12dB
# AC Analysis :

<img width="1912" height="690" alt="Image" src="https://github.com/user-attachments/assets/7506a113-d023-4374-9d5b-dc28e06b3542" />

 1. Midband Voltage Gain:
- midband gain=25.33dB
- |Av|dB = 20 log10(|Av|)
  |Av| = 10^(25.33/20)
  |Av| ≈ 18.47 V/V


3. −3 dB Cutoff Frequency (Bandwidth):
 - The bandwidth is determined by the frequency at which the gain drops by 3 dB from its maximum midband value.  
 - that is frequency at (25.33-3)dB which is **343.332MHz**
4. Unity Gain Frequency (fT):
   - This is the frequency at which the amplifier stops amplifying and the gain drops to 0 dB (a linear gain of 1 V/V).
   - frequency at 45dB is **490MHz**




# Inferance:
Circuit 1: 
- Resistive Source Degeneration Element: A standard passive resistor ($R_1 = 1\text{k}\Omega$).
- Characteristics: This is the classical approach. The resistor provides linear feedback, stabilizing the DC operating point and increasing the input range. However, in integrated circuit (IC) design, passive resistors like this can consume a significant amount of silicon area.

Circuit 2:
- Current Source Degeneration Element: An NMOS transistor ($M_3$) biased with a constant DC voltage ($V_3 = 0.61\text{V}$) at its gate.
- Characteristics: As long as $M_3$ is biased in the saturation region, it acts as a constant DC current source. This provides a very high incremental (AC) resistance while allowing you to control the exact DC tail current flowing through the amplifier.

Circuit 3: Diode-Connected Source Degeneration
- Degeneration Element: An NMOS transistor ($M_3$) configured as a "diode-connected" device (its gate is tied directly to its drain).
- Characteristics: A diode-connected transistor is always in saturation and acts as an active resistor. Its small-signal resistance is approximately $1/g_{m3}$. This is highly preferred in CMOS IC design because it replaces the bulky passive resistor from Circuit 1 with a much smaller MOSFET that scales well with the rest of the circuit.

  ### Comparission Table 
| Parameter | Exp 2A | Exp 2B | Exp 2C |
|-----------|--------------|--------------|--------------|
| Source Element | Source Resistor (Rs) | Current Source Degeneration Element | Diode-Connected Source Degeneration |
| Equivalent Source Resistance (RS) | Resistor(1k) | r03 | 1/gm3 |
| Transconductance (Gm) | 1/(1+gm1​R1​) | gm1/(1+​ro3​gm1) ​​≈ro3​1 | gm1/(1+​​gm1/gm3) |
| Linearity | Excellent | Poor (for voltage amplification) | Moderate to Good|
| Theoretical Gain (V/V) |15.38  |6.93  | 33.97 |
| Simulated Gain (V/V) |12.82  | 3.68 |18.47  |
| Simulated Gain (dB) | 22.17  | 11.35 | 25.33 |
| Bandwidth |  182.45MHz |  135.27MHz |  343.33MHz |  

    
        



  
  

