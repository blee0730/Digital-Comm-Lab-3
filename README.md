# Digital-Comm-Lab-3
## Introduction
In this lab GNURadio was used to create an fsk (Frequency Shift Keying) transmitter (Tx) and receiver (Rx). Unlike the previous labs this flowchart did not use the SDR and was solely made using GNURadio. Therefore, instead of using the SDR as an input it was instead replaced by a vector block that created a square wave to simulate a digital signal being transmitted. The flowchart is shown below.

## Flowchart
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/e3905628-1758-4d7a-a432-f3716d50ad1f)
This is the complete flowchart that was used in this lab which will be broken down and explained in parts. The big picture split of this flowchart is that everything up to the multiplication block is the transmitter and everything after is the receiver.

### Vector Source
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/2b83ad2e-2c43-4ff7-8967-1aa2e46a2923)

The vector source block is providing the system with a set of numbers that indicate whether the square wave input is low or high. There are only two levels for this lab meaning there are two bits of information being transmitted. The 1 represents the high (binary 1) which is the mark and the -1 represents the low (binary 0) which is the space and the square wave follows the pattern set by this vector source block. There is also a repeat interpolation block that sets the vector source to repeat the same pattern multiple times. If there is no oscilation between the two symbols the output of the digital signal is just a flat line as shown below:

![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/40282d1a-02b6-4c68-a970-4cdd753e34bc)


### Frequency Modulation
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/613faaef-511d-4193-8df5-f137d12b3f86)

The frequency modulation is controlled using multiple variables defined at the top of the flowchart. By changing the variable fsk_deviation_hz the frequency modulation sensitivity is changed in turn. This is shown clearly on the output using the first waterfall where the width of the waterfall is varied. This is the exact equation used inside of the frequency modulation block:

![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/7abd3133-f15c-43e2-9ad0-370e0b221827)

### Multiply Carrier
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/eb8420f0-2b68-473b-9aa9-816fc346831d)

This is setting a signal source at 2MHz frequency as the carrier and multiplying it with our digital signal coming from the vector source. The carrier frequency is much higher than that of the digital signal to avoid overmodulation. The throttle is there to ensure that the signal is cleanly output to the multiplier with the output of this multiplication being the Tx and the input of the Rx. The multiplication of this analog carrier and digital message outputs a modulated analog wave.

### Filter
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/f3cb1779-eac1-4a5b-8d7d-268c368a66ce)

This block is passing the multiplied analog carrier and digital square wave through a low pass filter. This signal is put through a waterfall sink which is the second waterfall shown on the output. This filter is similar to the ones used in lab 1 and 2 which have explained the use of low pass filtering. 

### Quadrature Demodulation
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/e6834d94-5d4a-4cb5-8ce8-18315aff40d1)

The quadrature demodulation block produces two baseband waveforms that represent the I and Q values of the message which is needed since the digital message is real and the analog carrier is complex. The exact equation inside of this block also uses the variable fsk_deviation_hz similar to the frequency modulation block which is shown below. This means that as the variable is changed using the slider shown on the output both the frequency sensitivity and the quadrature rate change.

![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/5768e548-ac13-417b-8717-270dbfa3f0f6)

### Binary Slicer
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/791b6f22-981b-47d7-9f52-ec08b6fa55c6)

The binary slicer takes the final modulated waveform float and converts it to symbols or binary 1's and 0's. The output of the slicer are characters thus there must be a character to float converter in order to see the output in time. Before the signal goes into the binary slicer it is added to a constant which is controlled by the variable "threshold". By increasing the threshold the width of the digital square wave decreases similarly by increasing the threshold the width increases.

### Output
![image](https://github.com/blee0730/Digital-Comm-Lab-3/assets/130094173/492e6eeb-a92e-4f64-89d2-d131a1fa6ad2)

The output shows the threshold and fsk_deviation_hz variables on top which can be changed by the user. The first waterfall output shows the transmitted signal or the signal that is being recieved. The second waterfall shows the signal after it gets filtered by a low pass filter. The final time sink shows the output signal in time that is the perfectly replicated original signal made from the vector source block. 
