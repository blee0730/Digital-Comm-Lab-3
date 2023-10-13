# Digital-Comm-Lab-3
## Introduction
In this lab GNURadio was used to create an fsk (Frequency Shift Keying) transmitter (Tx) and receiver (Rx). Unlike the previous labs this flowchart did not use the SDR and was solely made using GNURadio. Therefore, instead of using the SDR as an input it was instead replaced by a vector block that created a square wave to simulate a digital signal being transmitted. The flowchart is shown below.

## Flowchart
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/e3905628-1758-4d7a-a432-f3716d50ad1f)
This is the complete flowchart that was used in this lab which will be broken down and explained in parts. The big picture split of this flowchart is that everything up to the multiplication block is the transmitter and everything after is the receiver.

### Vector Source
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/2b83ad2e-2c43-4ff7-8967-1aa2e46a2923)

The vector source block is providing the system with a set of numbers that indicate whether the square wave input is low or high. There are only two levels for this lab meaning there are two bits of information being transmitted. The 1 represents the high (binary 1) and the -1 represents the low (binary 0) and the square wave follows the pattern set by this vector source block. There is also a repeat interpolation block that sets the vector source to repeat the same pattern multiple times.

### Frequency Modulation
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/613faaef-511d-4193-8df5-f137d12b3f86)

The frequency modulation is controlled using multiple variables defined at the top of the flowchart. By changing the variable fsk_deviation_hz the frequency modulation sensitivity is changed in turn. This is shown clearly on the output using the first waterfall where the width of the waterfall is varied. This is the exact equation used inside of the frequency modulation block:
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/7abd3133-f15c-43e2-9ad0-370e0b221827)



### Multiply Carrier
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/eb8420f0-2b68-473b-9aa9-816fc346831d)

### Filter
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/f3cb1779-eac1-4a5b-8d7d-268c368a66ce)

### Quadrature Demodulation
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/e6834d94-5d4a-4cb5-8ce8-18315aff40d1)

### Binary Slicer
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/791b6f22-981b-47d7-9f52-ec08b6fa55c6)

### Output
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/492e6eeb-a92e-4f64-89d2-d131a1fa6ad2)
