[[Research]] [[Neuromorphic]] 
# Adaptive Exponential Integrate and Fire Model

- $\tau_m\frac{dV}{dt}=RI(t)+[E_m-V+\Delta_Texp(\frac{V-V_T}{\Delta_T})]-Rw$
- $\tau\frac{dw}{dt}=-a[V-E_m]-w+b\tau\delta(t-t^f)$
- $\Delta_T$ around 1mV for pyramidal neurons
- Once potential crosses $V_T$, diverges to infinity in finite time
- Simulation reset to $V_r$ at this point
- Adaptation  reduces firing rate in presence of constant input
- Strong experimental evidence
- Can fit broad spectrum of behaviors
	- Adaptation, bursting, initial bursting, irregular firing, regular firing
- ![Pasted image 20210607195925.png](Pasted%20image%2020210607195925.png)
- ![Pasted image 20210607200032.png](Pasted%20image%2020210607200032.png)

## Building Ad. and Exp. Circuits on top of LIF
- ![Pasted image 20210627171111.png](Pasted%20image%2020210627171111.png)

### Exponential
- Weak inversion -> exponential relationship
- $I_d=I_0\frac{W}{L}exp(V_{gs}-V_{th}/nU_T)$
- ![Pasted image 20210627172704.png](Pasted%20image%2020210627172704.png)
- M3 receives subthreshold inverted voltage
- Mirrored and scaled by M4,5,6-9
- ![Pasted image 20210627172821.png](Pasted%20image%2020210627172821.png)

### Adaptation
- ![Pasted image 20210627173043.png](Pasted%20image%2020210627173043.png)
- Implements w adaptation equations
- Tunable drain-bulk floating resistor
	- ![Pasted image 20210627173639.png](Pasted%20image%2020210627173639.png)
- Spike Triggered Adaptation
	- ![Pasted image 20210627173659.png](Pasted%20image%2020210627173659.png)

## Behaviors
![Pasted image 20210627173737.png](Pasted%20image%2020210627173737.png)
