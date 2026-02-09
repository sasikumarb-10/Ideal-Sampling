# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
1.Computer with i3 processor
2.Python Colab

# Program
``` python
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter, filtfilt

# ---------------- IDEAL SAMPLING ----------------
fs1 = 100
f = 5
t1 = np.arange(0, 1, 1/fs1)
x1 = np.sin(2*np.pi*f*t1)

plt.figure(figsize=(10,3))
plt.plot(t1, x1)
plt.title("Ideal Sampling - Continuous Signal")
plt.grid()
plt.show()

plt.figure(figsize=(10,3))
plt.stem(t1, x1)
plt.title("Ideal Sampling")
plt.grid()
plt.show()

t1r = np.linspace(0, 1, 1000)
x1r = np.interp(t1r, t1, x1)

plt.figure(figsize=(10,3))
plt.plot(t1r, x1r)
plt.title("Ideal Sampling - Reconstructed Signal")
plt.grid()
plt.show()

# ---------------- NATURAL SAMPLING ----------------
t2 = np.linspace(0, 1, 1000)
x2 = np.cos(2*np.pi*5*t2)
p = ((t2*50) % 1 < 0.5)
xn = x2 * p

b, a = butter(4, 10/(0.5*1000))
xr2 = lfilter(b, a, xn)

plt.figure(figsize=(10,2))
plt.plot(t2, x2)
plt.title("Natural Sampling - Message Signal")
plt.grid()
plt.show()

plt.figure(figsize=(10,2))
plt.plot(t2, p)
plt.title("Natural Sampling - Pulse Train")
plt.grid()
plt.show()

plt.figure(figsize=(10,2))
plt.plot(t2, xn)
plt.title("Natural Sampling")
plt.grid()
plt.show()

plt.figure(figsize=(10,2))
plt.plot(t2, xr2)
plt.title("Natural Sampling - Reconstructed Signal")
plt.grid()
plt.show()

# ---------------- FLAT-TOP SAMPLING ----------------
fs3 = 1000
t3 = np.linspace(0, 1, fs3)
x3 = np.sin(2*np.pi*5*t3)

Ts = fs3 // 50
n = np.arange(0, fs3, Ts)
xh = np.repeat(x3[n], Ts)[:fs3]

b, a = butter(4, 10/(0.5*fs3))
xr3 = filtfilt(b, a, xh)

plt.figure(figsize=(10,3))
plt.plot(t3, x3)
plt.title("Flat-Top Sampling - Message Signal")
plt.grid()
plt.show()

plt.figure(figsize=(10,3))
plt.stem(t3[n], x3[n], basefmt=" ")
plt.title("Flat-Top Sampling - Sampling Instants")
plt.grid()
plt.show()

plt.figure(figsize=(10,3))
plt.plot(t3, xh)
plt.title("Flat-Top Sampling")
plt.grid()
plt.show()

plt.figure(figsize=(10,3))
plt.plot(t3, xr3)
plt.title("Flat-Top Sampling - Reconstructed Signal")
plt.grid()
plt.show()

```
# Output Waveform
**IDEAL SAMPLING**

<img width="707" height="742" alt="image" src="https://github.com/user-attachments/assets/c25597d2-b214-4605-bda4-ceb81b2461f7" />

**NATURAL SAMPLING**

<img width="708" height="726" alt="image" src="https://github.com/user-attachments/assets/c512843b-8233-4ccc-a019-42f8c3bbf40c" />

**FLAT-TOP SAMPLING**

<img width="528" height="740" alt="image" src="https://github.com/user-attachments/assets/01cae905-84d5-47b3-8d4d-b993007b1fe2" />

# Results
Thus, the python program for ideal sampling, natural sampling and flat-top sampling has been executed and verified successfully.
