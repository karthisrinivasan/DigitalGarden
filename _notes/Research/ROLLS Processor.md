[[Research]] [[Neuromorphic]] 

# A Reconfigurable Online Learning Spiking Neuromorphic Processor comprising 256 Neurons and 128K Synapses

[[Giacomo Indiveri]] 

- Integration of analog bistable learning synapses with asynchronous digital logic
- Enables arbitrary connectivity schemes

## Materials and Methods
### Processor Architecture
- ![Pasted image 20210606183008.png](Pasted%20image%2020210606183008.png)
- 256 neurons
- 256x256 long-term learning synapses
- 256x256 programmable synapses
- 256x2 virtual synapses for modeling shared synaptic weights
- [[AdExp I&F]] neurons
- bistable weights with LTP and LTD
- ![Pasted image 20210606183320.png](Pasted%20image%2020210606183320.png)
- ![Pasted image 20210606183336.png](Pasted%20image%2020210606183336.png)
- Programmable switch matrix controls connectivity

#### Synapse Temporal Dynamics
- Real-time operation -> Need to implement wide variety of time constants 
	- Differential-pair Integrator

#### Spike-based Learning Algorithm
- Timing-codes are not sufficient (???)
- New algorithm depends on
	- Spike timing
	- Post-synaptic potential
	- Recent spiking activity of post-synaptic neuron
- Requires stochastic update mechanism
- $w_i=w_i+\Delta w^+ \; if\; V_{mem}(t_{pre})>\theta_{mem} \;and\; \theta_1<Ca(T_{pre})<\theta_3$
- $w_i=w_i-\Delta w^- \; if\; V_{mem}(t_{pre})<\theta_{mem} \;and\;\theta_1<Ca(T_{pre})<\theta_2$
- $\Delta w^+$,$\Delta w^-$: magnitude of increase/decrease
- $V_{mem}(T_{pre})$: post-synaptic potential at spike arrival time
- $\theta_{mem}$: Threshold to determine whether to increase or decrease
- $Ca(t_{pre})$: Calcium concentration of post-synaptic neuron
- Useful in extending memory lifetime, increasing capacity
- Internal variable dynamics:
	- $\frac{dw_i}{dt}=+C_{drift}\;if\;w_i>\theta_w\;and\;w_i<w_{max}$
	- $\frac{dw_i}{dt}=-C_{drift}\;if\;w_i<\theta_w\;and\;w_i>w_{max}$
- Actual weight:
	- $J_i=J_{max}f(w_i,\theta_J)$
	- $f$ is sigmoid / hard threshold with threshold $|theta_J$

### Processor Building Blocks
#### Silicon Neuron: [[AdExp I&F]]
- ![Pasted image 20210606191518.png](Pasted%20image%2020210606191518.png)
	- ! -> set by on-chip bias generator
- Possible behaviors
	- ![Pasted image 20210606191706.png](Pasted%20image%2020210606191706.png)
	- Different reset voltages, different refractory period
	- Frequency adaptive behavior, Bursting behavior
- Firing-input injection curve
	- ![Pasted image 20210606191823.png](Pasted%20image%2020210606191823.png)
	- Good mismatch performance -> soma FETs larger
- Post-synaptic plasticity circuits
	- ![Pasted image 20210606192129.png](Pasted%20image%2020210606192129.png)

#### Long-Term Plasticity Synapse
- ![Pasted image 20210606192349.png](Pasted%20image%2020210606192349.png)
	- A - pulse generator for AER
	- B - timing diagram for enabling broadcast and recurrent activation
	- C - Weight update and current generator blocks
- ![Pasted image 20210606192526.png](Pasted%20image%2020210606192526.png)

#### Short-Term Plasticity Synapse
- 2 bits -> 4 possible values
- 1 bit -> exc. / inh.
- ![Pasted image 20210606192923.png](Pasted%20image%2020210606192923.png)
	- Current converter and short-term depression blocks
- STD behavior:
	- ![Pasted image 20210606193110.png](Pasted%20image%2020210606193110.png)

#### I/O Blocks
- AER Blocks
- Quasi-delay-insensitive design

## Results
### Attractor Networks
- cf. [[Dynamic Field Theory#Attractors and Instabilities]]
- ![Pasted image 20210606193657.png](Pasted%20image%2020210606193657.png)

### Multi-Layer Perceptron
- DVS input for image classification
- ![Pasted image 20210606194017.png](Pasted%20image%2020210606194017.png)
- Most complex aspects disabled
- ![Pasted image 20210606194238.png](Pasted%20image%2020210606194238.png)

