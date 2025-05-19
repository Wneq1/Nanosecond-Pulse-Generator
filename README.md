# Nanosecond-Pulse-Generator
A nanosecond pulse generator is a device or electronic circuit designed to precisely generate pulses with extremely short durations, reaching the scale of single nanoseconds (1 ns = 10⁻⁹ seconds). Such a high time resolution is essential in many modern applications where extreme accuracy and fast operation are critical.

In practice, nanosecond generators are used in measurement systems, telecommunications, and scientific research, enabling control and synchronization of very rapid processes. They allow for the generation of short electrical pulses with precisely defined pulse width and rise time, which form the foundation for high-performance digital and analog circuits.

An example waveform output from such a generator is illustrated in the graphic below. It exhibits a shape similar to a normal distribution with very steep rising and falling edges, and an amplitude close to the circuit’s supply voltage.
![image](https://github.com/user-attachments/assets/5e7388b9-90e2-40a9-a563-24183cbad239)

Although the datasheet of the LT1721 chip includes an example schematic of such a generator, it requires a triggering pulse from an external excitation generator. The author decided to design a circuit based on easily available and inexpensive components commonly found on the Polish market.

The schematic of the generator is presented below:
![image](https://github.com/user-attachments/assets/35a3b197-1607-4ca0-83bc-d39af512ef16)

The generator will consist of four basic blocks. The first block is a rectangular (square) wave signal generator. The next block is a delay line, followed by a block responsible for the exclusive alternative (exclusive OR). Finally, at the very end, there is a buffer that increases the current-driving capability of the generator’s output.
