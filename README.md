# Nanosecond-Pulse-Generator
A nanosecond pulse generator is a device or electronic circuit designed to precisely generate pulses with extremely short durations, reaching the scale of single nanoseconds (1 ns = 10⁻⁹ seconds). Such a high time resolution is essential in many modern applications where extreme accuracy and fast operation are critical. In practice, nanosecond generators are used in measurement systems, telecommunications, and scientific research, enabling control and synchronization of very rapid processes. They allow for the generation of short electrical pulses with precisely defined pulse width and rise time, which form the foundation for high-performance digital and analog circuits.

An example waveform output from such a generator is illustrated in the graphic below. It exhibits a shape similar to a normal distribution with very steep rising and falling edges, and an amplitude close to the circuit’s supply voltage.
![image](https://github.com/user-attachments/assets/5e7388b9-90e2-40a9-a563-24183cbad239)

Although the datasheet of the LT1721 chip includes an example schematic of such a generator, it requires a triggering pulse from an external excitation generator. The author decided to design a circuit based on easily available and inexpensive components commonly found on the Polish market. Currently, the LT1721 chip is difficult to obtain in the country, which necessitates searching for alternative components.

The schematic of the generator is presented below:

![image](https://github.com/user-attachments/assets/35a3b197-1607-4ca0-83bc-d39af512ef16)

The generator will consist of four basic blocks. The first block is a rectangular (square) wave signal generator. The next block is a delay line, followed by a block responsible for the exclusive alternative (exclusive OR). Finally, at the very end, there is a buffer that increases the current-driving capability of the generator’s output.

Rectangular Wave Generator Circuit:
The simplest rectangular wave generator circuit can be built using just three components: a resistor, a capacitor, and a NOT gate with a Schmitt trigger input. Circuits equipped with a Schmitt trigger input are characterized by hysteresis. Hysteresis is a phenomenon where the gate switches at different threshold voltage levels for the rising and falling edges of the signal. Therefore, for circuits with a Schmitt trigger input, threshold voltages for both edges and the hysteresis range are specified.

![image](https://github.com/user-attachments/assets/49f4c7e1-2c06-4134-b230-ce39b0c8db2c)

The simplest generator circuit is shown above. The operating principle of this circuit is very straightforward. Let’s assume that the switching thresholds of the Schmitt trigger gate are as follows: it switches from 1 to 0 when the input voltage exceeds 1.6 V, and from 0 to 1 when it drops to 0.8 V.

At the very beginning, the capacitor is discharged, so the voltage at the input is 0 V, which is lower than the 0.8 V threshold required to switch from 0 to 1. Therefore, the output is at a high state. When the output is high, the capacitor starts charging through the resistor until the voltage exceeds 1.6 V, triggering a state change. This cycle repeats continuously.

The operating frequency is determined by the following formula, where C1 is the capacitance of the oscillating capacitor, and R1 is the resistance value in the feedback loop:

$f_0 = 1.2 / (R_1 * C_1)$

​Delay Line:
The primary purpose of the delay line is to deliver two signals to the exclusive OR (XOR) circuit with an appropriate time shift. In this project, the output from the generator is fed directly into the XOR gate, while the second connection is realized through two NOT gates. It should be noted that the signals at the input of the path have the same phase but are slightly delayed due to the use of the double NOT gates. The signal delay time depends solely on the propagation delays of the NOT gates used, which provide the necessary timing difference.
