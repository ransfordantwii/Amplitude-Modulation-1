# Amplitude-Modulation-1
This is a project in which a message signal was being modulated by a carrier signal of a frequency and then concerted back to  its original form through the process of demodulation.
Code Explanation
1. System Parameters

This section defines the fundamental parameters that govern the sampling and transmission of the signals.

fc = 10e3;

Sets the Carrier Frequency (f 
c
​	
 ) to 10,000 Hz (or 10 kHz). This is the high frequency used to carry the message signal.

fs = 80e3;

Sets the Sampling Frequency (f 
s
​	
 ) to 80,000 Hz (or 80 kHz). This determines the digital resolution of the signals and must be high enough (at least twice the highest frequency component) to prevent aliasing.

t = (0:1/fs:0.01)';

Creates the Time Vector t. It defines the simulation duration (from 0 to 0.01 seconds) and the time steps (1/f 
s
​	
 ).

2. Message Signal (s)

This is the information (or audio) signal that will be transmitted.

s = sin(2*pi*300*t) + 2*sin(2*pi*600*t);

Creates the Baseband Message Signal s. It is composed of the sum of two pure sine waves: one at 300 Hz (with an amplitude of 1) and another at 600 Hz (with an amplitude of 2).

3. Filter Design

This step prepares a necessary component for the receiver.

[num,den] = butter(10, fc*2/fs);

Designs a 10th-order Butterworth Low-Pass Filter (LPF). This filter will be used in the demodulation step (amdemod) to isolate the low-frequency message signal after it is recovered.

4. Modulation (y)

This is the transmission stage, where the message is shifted to the high carrier frequency.

y = ammod(s, fc, fs);

Performs Standard Amplitude Modulation (AM) on the message signal s, using the defined carrier frequency f 
c
​	
  and sampling frequency f 
s
​	
 . The output, y, is the transmitted AM waveform.

5. Demodulation (z)

This is the reception stage, where the original message is recovered.

z = amdemod(y, fc, fs, 0, 0, num, den);

Performs Envelope Demodulation on the received signal y. The two zeros specify the default carrier amplitude (1) and initial phase (0) used during modulation. The coefficients num and den apply the LPF to the resulting signal, removing unwanted high-frequency components and yielding the recovered message signal, z.
