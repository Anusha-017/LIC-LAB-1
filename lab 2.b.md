# Experiment 2B:  Design CS amplifier with PMOS active load and NMOS current source degeneration in LTSPICE.

## Circuit Diagram:

<img width="1186" height="808" alt="Image" src="https://github.com/user-attachments/assets/91f81471-568a-4606-91e1-0a22780771d6" />

## Design Calculation:
# CMOS Amplifier Design Calculations

This section details the theoretical hand-calculations used to bias the **Common-Source amplifier with a PMOS active load and an NMOS current sink**.

---

# 1. Target Specifications & Given Parameters

Before sizing the transistors, the following process parameters and target operating conditions were defined.

- **Supply Voltage (VDD)** = 2 V  
- **Target Drain Current (ID)** = 200 µA  
- **Target Overdrive Voltage (VOV)** = 0.25 V (assumed uniform for all transistors)  
- **NMOS Threshold Voltage (Vthn)** = 0.36 V  
- **PMOS Threshold Voltage (|Vthp|)** = 0.39 V  

---

# 2. DC Biasing Calculations

## Biasing MOSFET 2 (PMOS Active Load – M2)

The PMOS transistor **M2** acts as the active load.  
Its source is connected to **VDD**.

- Source-to-Gate Voltage

VOV2 = VSG2 − |Vthp|

0.25 = VSG2 − 0.39

VSG2 = 0.64 V

- Gate Bias Voltage

VS2 − VG2 = 0.64

2.0 − VG2 = 0.64

VG2 = 1.36 V

**Result**

VB1 = 1.36 V  

This corresponds to the **DC source V4 in the LTspice schematic**.

---

## Biasing MOSFET 3 (NMOS Current Sink – M3)

The NMOS transistor **M3** sets the bias current for the branch.  
Its source is connected to **ground**.

-  Gate-to-Source Voltage

VGS3 = VOV + Vthn

VGS3 = 0.25 + 0.36

VGS3 = 0.61 V

- Gate Bias Voltage

Since VS3 = 0

VG3 = 0.61 V

**Result**

VB2 = 0.61 V  

This corresponds to **DC source V3 in the LTspice schematic**.

-  Saturation Condition Check

For M3 to remain in saturation

VDS3 ≥ VOV

VD3 − 0 ≥ 0.25

Design assumption

VS1 = VD3 ≈ 0.3 V

This ensures M3 stays safely in saturation.

---

## Biasing MOSFET 1 (NMOS Driver – M1)

M1 is the **main amplifying transistor**.

Its source is connected to the drain of **M3**.

VS1 = 0.3 V

- Gate-to-Source Voltage

VGS1 = VOV + Vthn

VGS1 = 0.25 + 0.36

VGS1 = 0.61 V

 - Input Bias Voltage

VG1 − VS1 = 0.61

VG1 − 0.3 = 0.61

VG1 = 0.91 V

**Result**

VIN = 0.91 V  

This matches the **DC offset of the sine source V2 in LTspice**.

---

## Transistor Sizing (Width Calculation)

The MOSFET current equation is used:

ID = (1/2) μCox (W/L) (VOV)^2

Using:

ID = 200 µA  
VOV = 0.25 V  
L = 0.18 µm  

After substituting the **TSMC 0.18 µm process parameters**, the transistor widths are calculated.

---
| Transistor | Type | Width (W) | Length (L) |
|------------|------|-----------|-----------|
| M1 | NMOS Driver | 5 µm | 0.18 µm |
| M3 | NMOS Current Sink | 5 µm | 0.18 µm |
| M2 | PMOS Active Load | 11.8 µm | 0.18 µm |


---

## Final Bias Voltages

| Node | Voltage |
|-----|--------|
| VDD | 2.0 V |
| VB1 (PMOS Gate) | 1.36 V |
| VB2 (NMOS Sink Gate) | 0.61 V |
| VIN (Input Bias) | 0.91 V |
| VS1 | 0.3 V |

---


## DC Analysis:

<img width="845" height="560" alt="Image" src="https://github.com/user-attachments/assets/8ac02ca0-4b63-4993-8285-4a75b6388932" />

to set opperating point new mosfet Dimensions are

| Transistor | Type | Width (W) | Length (L) |
|------------|------|-----------|-----------|
| M1 | NMOS Driver | 16 µm | 0.18 µm |
| M3 | NMOS Current Sink | 16 µm | 0.18 µm |
| M2 | PMOS Active Load | 34.5 µm | 0.18 µm |
## DC sweep:

<img width="1917" height="537" alt="Image" src="https://github.com/user-attachments/assets/5ef4dc3b-6ebe-45e3-bccc-ad90ed7f249d" />

## Key Takeaways
* **Optimal Bias Point:** For maximum linear swing, the DC bias point (quiescent point) for the input should be set squarely in the middle of the active region, around **0.8V to 0.85V**.
* **Output Swing:** The maximum output swing is asymmetrical. It can swing close to the 2.0V rail but is clamped at roughly 0.45V on the lower end due to the stacked NMOS structure (the driver and the current sink).


## Transient Analysis:

<img width="1918" height="915" alt="Image" src="https://github.com/user-attachments/assets/1f34329b-bc10-4f6b-8c97-b40813db0dcc" />

<img width="1917" height="861" alt="Image" src="https://github.com/user-attachments/assets/0a93b008-4c88-4bad-856a-de6d9a55e7cc" />

- Vout (peak-to-peak)=70.97mV
- Vin (peak-to-peak)=19.25mV
- Gain(Av)=Vout/Vin=3.68 V/V
- Gain(dB)=20log(Av)=11.31



## AC Analysis:

<img width="1918" height="608" alt="Image" src="https://github.com/user-attachments/assets/d71324ce-7c75-49ff-b85b-5ea18701c49b" />

 1. Midband Voltage Gain:
- midband gain=11.35dB
- |Av|dB = 20 log10(|Av|)
  |Av| = 10^(11.35/20)
  |Av| ≈ 3.68 V/V

2. Low-Frequency Phase Shift:
    - The dotted red line represents the phase shift (read from the right Y-axis). In the flat midband region, the phase is exactly 180°.
    - This 180° shift perfectly confirms that your circuit is operating as an inverting amplifier, which is the defining characteristic of a Common-Source topology. When the input signal goes positive, the output signal goes negative.
3. −3 dB Cutoff Frequency (Bandwidth):
 - The bandwidth is determined by the frequency at which the gain drops by 3 dB from its maximum midband value.  
 - that is frequency at (11.35-3)dB which is **135.27MHz**
4. Unity Gain Frequency (fT):
   - This is the frequency at which the amplifier stops amplifying and the gain drops to 0 dB (a linear gain of 1 V/V).
   - frequency at 45dB is **490MHz**

## Conclusion:
In this experiment, a **CMOS Common-Source amplifier with a PMOS active load and an NMOS current sink** was designed and analyzed using **LTspice with the TSMC 0.18 µm technology library**.

The biasing network was calculated to ensure that all MOSFETs operate in the **saturation region**, which is essential for proper analog amplification. The calculated bias voltages were implemented in the LTspice schematic and verified using **DC operating point analysis**.









