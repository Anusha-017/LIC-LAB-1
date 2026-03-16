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
        =



  
  

