[[Research]] [[Neuromorphic]]

# A Low Supply-Noise Neuron
[[Timothy Horiuchi]]

![Pasted image 20210614164902.png](Pasted%20image%2020210614164902.png)

Constant current draw on Vdd even during spike

Spike current drawn from digital Vdd line

Positive feedback thru PMOS generates (negative) spike when vmem near vthresh

Negative spike also charges 50fF to set refractory period, controlled by refr

Add R or MOSFET at vmem for leak

Sizes: (in micrometer, old tech. node)
M1, M2 = 2.4/1.8 
M3 = 2.4/2.1
M4 = 3.9/2.4
M5 = 3.6/3.6
M6, M7 = 2.4/1.8
M8 = 3.0/2.4

