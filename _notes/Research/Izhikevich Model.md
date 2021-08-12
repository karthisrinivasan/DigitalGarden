[[Research]] [[Neuroscience]] [[Neuromorphic]] [[MITACS Project]]

# Simple Model of Spiking Neurons

[[Eugene Izhikevich]]

- Plausible like HH model, efficient like LIF
- Bifurcation theory, Quadratic IF neuron

## The Model
- $\dot{v}=0.04v^2+5v+140-u+I$
- $\dot{u}=a(bv-u)$
- if $v\geq 30mV$, then $v$<-$c$ and $u$<-$u+d$
- $v$: membrane potential
- $u$: membrane recovery and provides negative feedback
- parameters obtained by fitting to cortical neuron data
- a: recovery time scale, typically 0.02
- b: sensitivity to subthreshold fluctuations of v
	- greater value => greater coupling
	- typically 0.2
- c: reset potential, typically -65mV
- d: reset of u,  typically 2
- ![Pasted image 20210602183730.png](Pasted%20image%2020210602183730.png)
- ![Pasted image 20210602183852.png](Pasted%20image%2020210602183852.png)

## Types of Dynamics
- ![Pasted image 20210613092702.png](Pasted%20image%2020210613092702.png)
- Regular spiking (RS)
	- most common
	- spike frequency adaptation
	- c=-65mV, d=8
- Intrinsically Bursting (IB)
	- burst followed by repetitive single spikes
	- c=-55mV d=4
- Chattering (CH)
	- Burst of closely spaced spikes
	- c=-50mV d=2
- Inhibitory: Fast Spiking (FS)
	- No adaptation
	- periodic trains
	- a=0.1
- Inhibitory: Low Threshold Spiking (LTS)
	- With spike adaptation
	- Low threshold b-0.25
- Thalamo-cortical (TC)
	-	Rest -> depolarized : tonic firing
	-	hyper-polarized : rebound burst
-	Resonator (RZ)
	-	a=0.1 b=0.26
	-	Bistability 

## Pulse Coupled Implementation
- 10k neurons, 1M synapses
- 4:1 excitatory:inhibitory connection number
- Randomly distributed between RS and CH parameters
- ![Pasted image 20210602184641.png](Pasted%20image%2020210602184641.png)
- Cortex-like dynamics
- Mean firing rate ~8Hz
- Self organization into assemblies despite range initializations