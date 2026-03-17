# EXPERIMENT 3 : To study and measure the characteristics and parameters of an Op-amp (IC-741):

## Aim:

To study and measure the characteristics and parameters of an Op-amp (IC-741):
(a) Input bias current at inverting terminal
(b) Input bias current at non-inverting terminal
(c) Input offset current
(d) Input offset voltage
(e) Slew rate

## Theory:

The operational amplifier is a versatile device that can be used to amplify dc as well as ac input signals and was originally designed for performing mathematical operations such as addition, subtraction, multiplication and integration. Thus, the word operational amplifier stems for its original use for these mathematical operations and is abbreviated to op-amp. With the addition of suitable external feedback components, the modern day op-amp can be used for a variety of applications, such as ac and dc signal amplification, active filters, oscillators, comparators, regulators and others.

Since an op-amp is a multistage amplifier, it can be represented by a block diagram as shown:

<img width="898" height="288" alt="Image" src="https://github.com/user-attachments/assets/8c71d0ca-7f1f-49e2-bb6b-e2c345d46de7" />
The input stage is the dual input, balanced-output differential amplifier. This stage generally provides most of the voltage gain of an amplifier and also establishes the input resistance of the op-amp. The intermediate stage is usually another differential amplifier, which is driven by the output of the first stage. 
The final stage is usually a push-pull complementary amplifier output stage. The output stage increases the output voltage swing and raises the current supplying capability of the op-amp. A well-designed output stage also provides low output resistance.

the schematic symbol of an op-amp:

<img width="662" height="376" alt="Image" src="https://github.com/user-attachments/assets/58e7094c-422c-49cd-ab19-85110abee277" />

The input differential amplifier stage of the op-amp is designed to be operated in the differential mode, the differential inputs are designated by the (+) and (-) notations. The (+) input is the non-inverting input. An ac signal (or dc voltage) applied to this input produces an in-phase (or same polarity) signal at the output. On the other hand, the (-) input is the inverting input because an ac signal (or dc voltage) applied to this input produces a 180° out of phase (or opposite polarity) signal at the output.

## Measurement Inverting bias current :
Circuit Diagram:

<img width="372" height="347" alt="Image" src="https://github.com/user-attachments/assets/bf044d79-2c9a-4c63-875d-1b9845eed6d4" />

### STEPS:
- Click on the components button to place the component on the table.
- Make connections as per the circuit diagram.
- Click on 'Check Connection' button to check connections. If correct, Click on 'Show output voltage' button to view output on DMM.
- Calculate the inverting bias current using the formula:
      IB1 = Vo/Rf
          =0.024/470k
          =**0.05uA**
- Click on 'Result' button and enter the claculated value.
- Click on 'Reset' button and proceed in the same way to calculate the input bias current at non-inverting terminal.

<img width="1058" height="686" alt="Image" src="https://github.com/user-attachments/assets/77ab8eea-6de6-4088-8e59-397b272dc0d4" />

## Measurement of non-inverting bias current IB2

Circuit Diagram:

<img width="708" height="560" alt="image" src="https://github.com/user-attachments/assets/2a4b1f4e-42e9-43f6-bb83-ecfed4075c2a" />

### STEPS:
- Click on the component button to place the component on the table.
- Make connections as per the circuit diagram.
- Click on 'Check Connection' button to check connections. If correct, Click on 'Show output voltage' button to view output on DMM.
- Calculate the non-inverting bias current using the formula:
           IB2 = Vo/R1
               =0.02/470k = **0.042 uA**
- Click on 'Result' button and enter the claculated value.
- The input bias current IB hence, can be calculated using the formula:
IB = (IB1 + IB2)/2(where, IB1 has to be calculated from previous part)

  = (0.05*10^-6+0.0042*10^-6)/2= **0.046uA**

<img width="1107" height="617" alt="Image" src="https://github.com/user-attachments/assets/41d5a83b-1b69-41ad-80a0-3e4267246ddc" />


## Measurement of input offset current

Circuit Diagram:

<img width="395" height="316" alt="image" src="https://github.com/user-attachments/assets/25509c1d-719e-43b6-a295-c364b97bdbf4" />

### STEPS:

- Make connections as per the circuit diagram.
- Click on 'Check Connection button to check connections. If correct, Click on 'Show output voltage' button to view output on DMM.
- Calculate the input offset current using the formula:
Iio = Vo/Rf = 0.003/470k=**0.0063uA**
- Click on 'Result' button and enter the claculated value.

<img width="987" height="548" alt="image" src="https://github.com/user-attachments/assets/cc8a6cb2-9324-4e14-b77e-1e0242ab08d1" />

## Measurement of input offset voltage

<img width="670" height="552" alt="image" src="https://github.com/user-attachments/assets/d0f4a622-ef80-4c43-b2e4-56aa1435b206" />

### STEPS
- Make connections as per the circuit diagram.
- Click on 'Check Connection' button to check connections. If correct, Click on 'Show output voltage' button to view output (Vo) on DMM.
- Calculate the input offset voltage, Vio using the formula:
Vio = (Vo - IioRf)/(1+Rf/Ri) =1.048mV
- Click on 'Result' button and enter the claculated value.

## Measurement of slew rate 

Circuit Diagram:

<img width="355" height="316" alt="image" src="https://github.com/user-attachments/assets/b513adac-e45b-4ba3-a1dd-9ee38892ae16" />

### STEPS
- Make connections as per the circuit diagram.
- The input signal* has to be taken from the red terminal of A.F. Oscillator while the other terminal has to be grounded.
- Also, feed the input signal to channel CH1 of the C.R.O and the output from Op-Amp IC must be fed to the channel CH2.
- Click on 'Check Connection' button to check connections. If correct, Click on 'Show output voltage' button to view output.
- Increase the frequency of input signal using the dial** on A.F. Oscillator until output wave becomes triangular. This is the required frequency fmax in KHz.
- Calculate the slew rate using the formula:
S.R. = 2πfmaxVm/106   V/μs
Click on 'Result' button and enter the calculated value.

<img width="864" height="504" alt="image" src="https://github.com/user-attachments/assets/3528ce24-d65c-4538-bc45-d1668ebaa7e5" />


<img width="940" height="551" alt="image" src="https://github.com/user-attachments/assets/a3d5510a-f2c4-4873-b5f8-a5e9dc5f460d" />



  
  
  
