[[Research]] [[Neuromorphic]]

# A VLSI Array of Low-Power Spiking Neurons and Bistable Synapses With Spike-Timing Dependent Plasticity

[[Giacomo Indiveri]] [[Elisabetta Chica]]

32 neurons, 32x8 synapses

## I&F Neuron
- ![Pasted image 20210618145536.png](Pasted%20image%2020210618145536.png)
-  Source follower M1-M2 ->  control spiking threshold 
-  Inverter with positive feedback M3-M7 -> reduce power consumption
-  Inverter with controllable slew-rate M8-M11 -> arbitrary refractory periods
-  Inverter M12-M13 -> generate digital pulses
- Current integrator M15-M19 for spike-frequency adaptation 
- M20 for setting a leak current
-  M21-M22 for receiving and producing the AER handshaking signals

## Bistable Synapse
- ![Pasted image 20210618150527.png](Pasted%20image%2020210618150527.png)
	- excitatory

## STDP Circuit
- ![Pasted image 20210618151442.png](Pasted%20image%2020210618151442.png)


