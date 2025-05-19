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

The simplest generator circuit is shown above. The operating principle of this circuit is very straightforward. Let’s assume that the switching thresholds of the Schmitt trigger gate are as follows: it switches from 1 to 0 when the input voltage exceeds 1.6 V, and from 0 to 1 when it drops to 0.8 V. At the very beginning, the capacitor is discharged, so the voltage at the input is 0 V, which is lower than the 0.8 V threshold required to switch from 0 to 1. Therefore, the output is at a high state. When the output is high, the capacitor starts charging through the resistor until the voltage exceeds 1.6 V, triggering a state change. This cycle repeats continuously.
The operating frequency is determined by the following formula, where C1 is the capacitance of the oscillating capacitor, and R1 is the resistance value in the feedback loop:

$f_0 = 1.2 / (R_1 * C_1)$

​Delay Line:

The primary purpose of the delay line is to deliver two signals to the exclusive OR (XOR) circuit with an appropriate time shift. In this project, the output from the generator is fed directly into the XOR gate, while the second connection is realized through two NOT gates. It should be noted that the signals at the input of the path have the same phase but are slightly delayed due to the use of the double NOT gates. The signal delay time depends solely on the propagation delays of the NOT gates used, which provide the necessary timing difference.

![image](https://github.com/user-attachments/assets/29a8d6e0-926f-4c29-aee4-abd5d49f3a6e)

XOR Gate:

The XOR gate generates a short pulse (called a spike pulse) each time there is an edge on the output signal of the relaxation oscillator. Based on the XOR truth table, when its inputs are at different logic levels (one input is high while the other is delayed by the NOT inverters), the output goes high. This high state lasts until the delayed input also changes state, effectively turning off the generator. When both inputs are either high or low simultaneously, the output remains at 0, producing no pulse. These pulses appear in pairs, as each pulse corresponds to both the rising and falling edges of the oscillator’s output signal. The XOR gate is used here for precise detection of signal state changes, enabling the generation of very short output pulses.

![image](https://github.com/user-attachments/assets/1daba656-c69c-4344-b97e-21f7cfdcaf4d)

Output Buffer:

Since the output of the generator is not intended to drive a heavy load, it was decided to increase the current-driving capability of the circuit by adding additional NOT gates at the output. The typical current capability of a standard logic gate ranges from about 5 to 10 mA, so it was necessary to increase this capacity to protect the circuit from accidental overload.
At the output of the XOR gate, there is a NOT gate that inverts the input signal. Following this, the actual buffer consists of three NOT gates connected in parallel. Resistors are placed at their outputs to provide impedance matching for the proper output, and a connector allows the addition of an external resistor if needed.

The complete generator schematic is shown below:

![image](https://github.com/user-attachments/assets/7043d8ed-1786-4c7d-9272-873e308068ac)

Selection of Integrated Circuits for the Generator:

When working with very fast logic circuits, it is crucial that their propagation delays are as short as possible. On the market, there are two main families of logic ICs widely used in digital electronics: HC (High-speed CMOS) and AC (Advanced CMOS). Both are based on CMOS technology but differ primarily in speed and power consumption, which determines their suitability for various applications. Understanding these differences helps in selecting the appropriate family of ICs for specific uses, especially in hobbyist and student projects.

The HC family, which includes ICs like the 74HC04, is characterized by low power consumption and higher speed compared to traditional CMOS devices. HC ICs are voltage-compatible with TTL logic, allowing them to be used in systems combining different logic technologies. They operate in a voltage range from 2 V to 6 V, making them versatile for low-voltage applications common in modern digital circuits. Due to their energy efficiency, HC gates are commonly used in projects requiring moderate speed with power savings.

The AC family, including ICs such as the 74AC86N, is an enhanced version of HC, offering significantly higher operating speeds. AC ICs have shorter propagation delays, making them ideal for applications requiring very fast switching. Although they consume slightly more power than HC devices, their high performance is essential in projects where response time is critical. They also operate within the same voltage range as HC (2 V to 6 V), maintaining versatility.

For the rectangular signal generator, the 74HCT14 gate was chosen because propagation delay is not a critical factor in this function, and it allows for a significant cost reduction. In contrast, the delay line and XOR modules use 74AC04N and 74AC86N gates. The use of AC gates results from more demanding tasks where delay time and XOR gate switching speed are crucial. The high-speed operation of these ICs enables precise signal control, which is especially important in this project. Additionally, the use of AC gates contributes to an energy-efficient design, with their low power consumption and simple power supply requirements (2 V to 6 V range) greatly simplifying the overall construction.

PCB Design:

The design will be carried out in the KiCad environment due to several key advantages. First and foremost, KiCad offers an intuitive and user-friendly interface that allows even beginners to start working on a project quickly. This makes the design process less time-consuming and more efficient.
Another important advantage of KiCad is the ability to visualize the project at every stage of work. This makes it easy to control the placement of components and routing of tracks, significantly minimizing the risk of errors and allowing for quick corrections. The software also provides extensive libraries of electronic components, which are regularly updated, greatly facilitating the selection and placement of the right parts. Additionally, KiCad allows easy generation of various production files such as Gerber files, drill files, and technical documentation, streamlining the process of ordering PCBs from manufacturers. It is also worth emphasizing that KiCad offers circuit simulation functionality, enabling preliminary testing of the circuit operation before creating a physical board. All these features together make using KiCad not only convenient but also economical and efficient.
