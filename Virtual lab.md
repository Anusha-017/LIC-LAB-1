# EXPERIMENT 3 : To study and measure the characteristics and parameters of an Op-amp (IC-741):

# Theory:

The operational amplifier is a versatile device that can be used to amplify dc as well as ac input signals and was originally designed for performing mathematical operations such as addition, subtraction, multiplication and integration. Thus, the word operational amplifier stems for its original use for these mathematical operations and is abbreviated to op-amp. With the addition of suitable external feedback components, the modern day op-amp can be used for a variety of applications, such as ac and dc signal amplification, active filters, oscillators, comparators, regulators and others.

Since an op-amp is a multistage amplifier, it can be represented by a block diagram as shown:

<img width="898" height="288" alt="Image" src="https://github.com/user-attachments/assets/8c71d0ca-7f1f-49e2-bb6b-e2c345d46de7" />
The input stage is the dual input, balanced-output differential amplifier. This stage generally provides most of the voltage gain of an amplifier and also establishes the input resistance of the op-amp. The intermediate stage is usually another differential amplifier, which is driven by the output of the first stage. 
The final stage is usually a push-pull complementary amplifier output stage. The output stage increases the output voltage swing and raises the current supplying capability of the op-amp. A well-designed output stage also provides low output resistance.

the schematic symbol of an op-amp:

<img width="662" height="376" alt="Image" src="https://github.com/user-attachments/assets/58e7094c-422c-49cd-ab19-85110abee277" />

The input differential amplifier stage of the op-amp is designed to be operated in the differential mode, the differential inputs are designated by the (+) and (-) notations. The (+) input is the non-inverting input. An ac signal (or dc voltage) applied to this input produces an in-phase (or same polarity) signal at the output. On the other hand, the (-) input is the inverting input because an ac signal (or dc voltage) applied to this input produces a 180° out of phase (or opposite polarity) signal at the output.

# Inverting bias current :

<img width="372" height="347" alt="Image" src="https://github.com/user-attachments/assets/bf044d79-2c9a-4c63-875d-1b9845eed6d4" />

### STEPS:
- Click on the components button to place the component on the table.
- Make connections as per the circuit diagram.
- Click on 'Check Connection' button to check connections. If correct, Click on 'Show output voltage' button to view output on DMM.
- Calculate the inverting bias current using the formula:
      IB1 = Vo/Rf
          =0.024/470k
          =0.05uA
- Click on 'Result' button and enter the claculated value.
- Click on 'Reset' button and proceed in the same way to calculate the input bias current at non-inverting terminal.

<img width="1058" height="686" alt="Image" src="https://github.com/user-attachments/assets/77ab8eea-6de6-4088-8e59-397b272dc0d4" />
