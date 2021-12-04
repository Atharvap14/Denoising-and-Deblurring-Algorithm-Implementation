# Denoising-and-Deblurring-Algorithm-Implementation
PROBLEM STATEMENT :
One of the many applications of Internet of Things (IoT) consists of continuous monitoring of
temperature in an area. To that end, several temperature sensors are installed at different
locations. These sensors measure and store the recorded value of temperature over time.
However, due to limitations of hardware, the sensor memory needs to be cleared periodically
and this is done by transmitting the stored values to a base unit. Assume that x[n] denotes the
samples of the true value of temperature recorded by a sensor. However, it is found that the
received signal y[n] at the base unit suffers from blur distortions and noise (additive). Hence, the
signal y[n] needs to be first processed so that we can recover x[n] from it. Assume that blur
happens via a system characterized by an impulse response h[n] = 1/16 [1 4 6 4 1] (assume
that the center value of 6/16 corresponds to n = 0). Then, implement the following two
approaches to recover the original signal x[n] from distorted signal y[n] :
1. First remove noise and then sharpen (deblur). Let the resulting signal be x1[n].
2. First sharpen (deblur) and then remove noise. Let the resulting signal be x2[n].
Now, compare x1[n] and x2[n] with x[n]. What conclusions can you draw from your
observations? Also, explain your observations from a theoretical perspective if possible.
APPROACH :
To recover original signal x[n] from y[n], following 2 approaches are used -
1) First remove the noise (Denoise) and then deblur to recover the original signal.
2) First deblur the distorted signal and then remove the noise (Denoise) to recover the
original signal.Analysis of Input Signal -
Input Signal Fourier Transform of Input Signal
We can see that the input signal comprises two major peaks in its fourier transform, one of
lower frequency and other of higher frequency and the fourier transform is also composed of
other frequencies but in lower amplitudes. Hence, they would have lower contributions.So, if we
are able to preserve the two peaks in its fourier transform, then we could retrieve the majority of
the signal. This shows us the possibility that a band reject filter rejects the frequencies which are
lower in amplitude between the two impulses.
Deblurring System -
Given a blurring system, it convolves the input signal with the inverse of the blurring system and
provides the deblurred signal as the output.
Working :
Fourier Transform of the given Blurring System
The above given plot represents the fourier transform of the Blurring system in the given
problem statement. We can see that the fourier transform approaches zero at the frequency of
Pi (2Pi/1000 * 500). Hence, the inverse system would have an impulse at this point. In order totake care of the situations when the fourier transform of the blurring system tends to zero, a
threshold is introduced which is close to zero.
Denoising Systems -
● Averaging Filter : It replaces the value of the signal at a point with the average of the
value of the signal at neighbouring points. For boundary cases, Padding is applied.
● Low Pass Filter : A filter that passes signals with a frequency lower than a selected
cutoff frequency and attenuates signals with frequencies higher than the cutoff frequency
● Amplitude Based Suppression : It suppresses the frequencies whose amplitude in the
signal’s fourier transform is less than the threshold frequency.
RESULT / THEORETICAL EXPLANATION :
A) Using Average Filter -
a) Task 1
First the signal is filtered and then deblurred. The filter replaces the value of the signal at a
point with the average of the value of the signal at 10 neighbouring points. For boundary cases,
zero padding is applied. The deblurring system takes the denoised signal and divides it fourier
transform with fourier transform of the blurring system and applies inverse fourier to retrieve the
output signal. The output signal is compared with the input signal and the RMSE value found is
972.39
The above shown result does not resemble the targeted input value due to ineffective denoising.
Since, averaging is unable to remove the noise efficiently, thus the deblurring system causes the
noise to be amplified and this results in the above signal plot which doesn’t resemble the
original signal.b) Task 2
Deblurring causes the noise to amplify and the signal becomes unusable. Now denoising is of
no use. The output signal is compared with the input signal and the RMSE value found is
289.23
B) Using Low Pass Filter -
a) Task 1
First the fourier transform of the input signal is found and it is passed through Low Pass Filter
and then deblurred. Since a low pass filter only allows frequencies lower than the cutoff
frequency to pass through which causes the loss of higher frequencies which are a part of the
signal. Hence a major component of energy of the signal is lost and which is seen in the above
plot where the output signal (orange graph) is very less when compared to the expected outputsignal (blue graph). The output signal is compared with the input signal and the RMSE value
found is 11.18
b) Task 2
First the input signal is deblurred and then it is passed through a low pass filter. The input signal
on deblurring has a high component of frequencies that make up noise. However, these
frequencies are greater than the cutoff frequency of low pass filter and hence are removed.
Also, the high frequency component of the input signal is lost. Thus the output signal (orange
plot) is similar to that of Task 1, with less energy and smaller than the expected output (blue
plot). The output signal is compared with the input signal and the RMSE value found is 11.18
C) Amplitude Based Filter -
Since the noise is a higher frequency component of a signal but with less amplitude in its fourier
transform (i.e., it does not contribute significantly to the signal). So, we designed an Amplitude
based filter that would remove the frequency components less than a particular threshold
amplitude.a) Task 1
First the input signal is passed through an amplitude based filter for denoising and then
deblurred. The amplitude based filter removes the frequencies that have low
contribution to the input signal. The denoised signal was then passed through the
deblurring system to get the output signal. In the above figure, the output signal (orange
plot) and the expected output signal (blue plot) are shown. It can be seen that the output
closely resembles the expected output signal. The output signal is compared with the input
signal and the RMSE value found is 2.94
b) Task 2
The input signal is first passed through a deblurring system and then through an amplitude
based filter in order to get the output signal. The deblurring system causes the amplification of
the frequencies constituting noise which renders the amplitude based filtering moot. The above
plot shows a comparison of the output signal (orange plot) and the expected output signal (blue
plot). The expected output signal is not visible since the noise has been amplified. The output
signal is compared with the input signal and the RMSE value found is 4486.07CONCLUSION :
RMSE VALUES
Deblurring is common in all the experiments. Denoising filters were varied.
For various denoising filters, we can conclude :
● In Average Filtering : RMSE value suggests that this method is not suitable for either
task and hence for processing the given input signal.
● In Low Pass Filtering : RMSE value suggests that this method is not suitable for either
task since it removes the higher frequency components of the signal. Hence, it is not
useful for processing the given input signal.
● In Amplitude Based Filtering : RMSE value suggests that this method is suitable for Task
1 (deblurring after denoising) however in Task 2 (denoising after deblurring) noise is
amplified.
Other Findings :
● Cascading the average filter and Amplitude Based filtering improves the RMSE values
and gives a more approximate output signal.
● A band pass filter would have been useful in both the tasks. However, it would have only
worked for the above given input signal and could not be implemented for processing a
different signal from the temperature sensor.
