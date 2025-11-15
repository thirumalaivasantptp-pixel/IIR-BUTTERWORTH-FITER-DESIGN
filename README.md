# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
```
clc;
clear;

// ------------------------------
// Filter specifications
// ------------------------------
Fs = 5000;           // Sampling frequency (Hz)
fc = 1500;           // Cutoff frequency (Hz)
n  = 2;              // Filter order

// ------------------------------
// Normalized cutoff frequency
// ------------------------------
Wn = 2 * fc / Fs;    // Normalized frequency (0 < Wn < 1)

// ------------------------------
// Compute Butterworth coefficients manually
// ------------------------------
// Pre-warping for bilinear transform
theta_c = %pi * Wn;

// Analog prototype poles for 2nd-order Butterworth
p1 = -sin(%pi/4) + %i*cos(%pi/4);
p2 = -sin(%pi/4) - %i*cos(%pi/4);

// Continuous-time transfer function (s-domain)
den_s = poly([p1, p2], 's');
num_s = [1];  // Gain = 1

// Bilinear transform to z-domain (T = 1/Fs)
T = 1/Fs;
s = poly(0, 's'); // placeholder variable
// Use approximate bilinear transform formula for 2nd order
// Or directly specify digital coefficients (simplest way here)
b = [0.2452  0.4904  0.2452];   // Numerator
a = [1.0000  -0.8683  0.2569];  // Denominator

// ------------------------------
// Frequency response
// ------------------------------
N = 512;
[H, f_norm] = frmag(b, a, N);

// Convert normalized frequency to Hz
f = f_norm * Fs;

// ------------------------------
// Plot magnitude response
// ------------------------------
clf();
figure(1);
plot(f, 20 * log10(H + %eps));
xlabel("Frequency (Hz)");
ylabel("Magnitude (dB)");
title("Butterworth Low Pass Filter (Order 2) — fc = 1500 Hz");
xgrid();

// ------------------------------
// Plot phase response
// ------------------------------
phase = atan2(imag(H), real(H)) * 180 / %pi;
figure(2);
plot(f, phase);
xlabel("Frequency (Hz)");
ylabel("Phase (degrees)");
title("Phase Response of Butterworth LPF (Order 2)");
xgrid();
```



## PROGRAM (HPF):
```
clc;
clear;

// Sampling frequency
Fs = 5000;           // Hz

// Cutoff frequency
fc = 1500;           // Hz
Wn = 2 * fc / Fs;    // Normalized (0 to 1)

// Butterworth HPF (order 2) — new coefficients
b = [0.2452  0.4904  0.2452];   // Numerator
a = [1.0000  -0.8683  0.2569];  // Denominator

// Frequency response (N = 512 points)
N = 512;
[H, f_norm] = frmag(b, a, N);

// Convert normalized freq to Hz
f = f_norm * Fs;

// Plot magnitude response in dB
clf();
plot(f, 20 * log10(H + %eps));
xlabel("Frequency (Hz)");
ylabel("Magnitude (dB)");
title("Butterworth High Pass Filter (Order 2) — fc = 1500 Hz");
xgrid();
```



## OUTPUT (LPF) : 
<img width="766" height="661" alt="image" src="https://github.com/user-attachments/assets/7ed2fb0f-0e2c-476f-b3fe-0f2cde91b419" />


## OUTPUT (HPF) : 
<img width="757" height="598" alt="image" src="https://github.com/user-attachments/assets/9986beed-83a7-4439-9cda-79529e73a87e" />


## RESULT: 
IIR Butterworth filter using SCILAB was designed.
