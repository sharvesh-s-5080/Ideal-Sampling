# Ideal, Natural, & Flat-top -Sampling
## Aim:
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
## Tools required:
  Google colab   
##  Theory
Ideal or Instantaneous or Impulse Sampling:
sampling signal is a periodic impulse train. The area of each impulse in the sampled signal is equal to the instantaneous value of the input signal.

Natural Sampling:
Natural sampling is also called practical sampling. In this sampling technique, the sampling signal is a pulse train. In natural sampling method, the top of each pulse in the sampled signal retains the shape of the input signal during pulse interval.

Flat Top Sampling:
The flat top sampling is also the practical sampling technique. In the flat top sampling, the sampling signal is also a pulse train. The top of each pulse in the sampled signal remain constant and is equal to the instantaneous value of the input signal 𝑥(𝑛) at the start of the samples.
## Ideal-Sampling Program:
```
import numpy as np, matplotlib.pyplot as plt
from scipy.signal import resample

fs, T, f = 100, 1, 5
t = np.arange(0, T, 1/fs)
x = np.sin(2*np.pi*f*t)

plt.figure(); plt.plot(t, x); plt.title("Continuous Signal"); plt.grid(); plt.show()

plt.figure(); plt.stem(t, x); plt.title("Impulse Sampling"); plt.grid(); plt.show()

xr = resample(x, len(t))
plt.figure(); plt.plot(t, xr); plt.title("Reconstructed Signal"); plt.grid(); plt.show()
```
## Ideal-Sampling Output Waveform
<img width="470" height="500" alt="image" src="https://github.com/user-attachments/assets/cb71b102-7154-4752-98f2-618bb53f3c40" />

## Natural-Sampling Program
```
import numpy as np, matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

fs,T,fm = 1000,1,5
t = np.arange(0,T,1/fs)
m = np.sin(2*np.pi*fm*t)

pr = 50
idx = np.arange(0,len(t),fs//pr)
flat = np.zeros_like(t)
w = fs//(2*pr)

for i in idx: flat[i:i+w] = m[i]

b,a = butter(5,10/(0.5*fs),'low')
rec = lfilter(b,a,flat)

plt.figure(figsize=(10,8))
plt.subplot(4,1,1); plt.plot(t,m); plt.title("Original Signal")
plt.subplot(4,1,2); plt.stem(t[idx],np.ones_like(idx)); plt.title("Sampling Points")
plt.subplot(4,1,3); plt.plot(t,flat); plt.title("Flat-Top Sampling")
plt.subplot(4,1,4); plt.plot(t,rec); plt.title("Reconstructed Signal")
plt.tight_layout(); plt.show()
```
## Natural-Sampling Output Waveform:
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/2511c924-392e-4c83-84ea-5d95f784a653" />


## Flat-top -Sampling Program:
```
import numpy as np, matplotlib.pyplot as plt
from scipy.signal import butter,lfilter

fs,T,fm=1000,1,5
t=np.arange(0,T,1/fs)
m=np.sin(2*np.pi*fm*t)

pr=50
pt=np.zeros_like(t)
w=fs//pr//2
for i in range(0,len(t),fs//pr): pt[i:i+w]=1

ns=m*pt
b,a=butter(5,10/(0.5*fs),'low')
rec=lfilter(b,a,ns)

plt.figure(figsize=(10,8))
plt.subplot(4,1,1); plt.plot(t,m); plt.title("Original Signal")
plt.subplot(4,1,2); plt.plot(t,pt); plt.title("Pulse Train")
plt.subplot(4,1,3); plt.plot(t,ns); plt.title("Natural Sampling")
plt.subplot(4,1,4); plt.plot(t,rec); plt.title("Reconstructed Signal")
plt.tight_layout(); plt.show()
```
## Flat-top -Sampling Output Waveform:
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/ff79973e-55ff-4ea9-b26c-066496194663" />

## Result:
Thus, the construction and reconstruction of Ideal, Natural, and Flat-top sampling were successfully implemented using Python, and the corresponding waveforms were obtained.
