[[Research]] [[Neuroscience]] [[Neuromorphic]] [[MITACS Project]]

# Low Power Circuit of an LIF Neuron with Global Reset

[[Jafar Shamsi]]

- Resistive load drive: 10k$\Omega$
- Power consumption: 2pJ/spike
	- At 1M$\Omega$ load
- 32pW static power
- Interface to reset membrane potential externally

## Proposed Circuit
- Two voltage sources only
- ![Pasted image 20210602190000.png](Pasted%20image%2020210602190000.png)

### Leaky Integrator
- $I_m$ injected through current mirror
	- Integrated by $C_u$ and leaked through M3
- input current ~10s of nA, time constant ~40us
- Response to input spike: 100ns,100nA
- ![Pasted image 20210602190315.png](Pasted%20image%2020210602190315.png)

### Spike Generator
- Low power Schmitt trigger
- O switches from high to low when threshold is reached
- M1 turned on; reset is through M4
- Spike Threshold:
	- $V_{SP}=V_{DD}\frac{(R_{nn}-1)}{R_{nn}(R_{np}+1)+1}+V_{th}\frac{R_{nn}(2R_{np}-1)-1)}{R_{nn}(R_{np}+1)+1}$
	- $R_{np}=\sqrt{\frac{\beta_{M7}}{\beta_{M5}}}$
	- $R_{nn}=\sqrt{\frac{\beta_{M9}}{\beta_{M7}}}$
- Spike generation for input current: 620mV threshold, 122ns 0.9V output spike
- ![Pasted image 20210602190827.png](Pasted%20image%2020210602190827.png)
- Reset through Grst, externally, if needed

### Results
- Power consumption
	- ![Pasted image 20210602190957.png](Pasted%20image%2020210602190957.png)
- Encoding: value -> spike rate
	- ![Pasted image 20210602191207.png](Pasted%20image%2020210602191207.png)
	- ![Pasted image 20210602191224.png](Pasted%20image%2020210602191224.png)
- Winner-Take-All 
	- Input layer that encodes inputs into spike trains
	- Fully connected to output layer
	- Output layer has lateral inhibition
	- In proposed circuit, output neurons connected to each other through global reset
	- ![Pasted image 20210602191440.png](Pasted%20image%2020210602191440.png)
- Synapse circuit
	- ![Pasted image 20210602191455.png](Pasted%20image%2020210602191455.png)
- Training:
	- 8x8 input neurons, 4 output neurons
	- STDP 
	- 1:1 allocation of neuron to pattern
	- Weights resemble pattern
		- ![Pasted image 20210602191617.png](Pasted%20image%2020210602191617.png)
	- 300us stimulation
	- ![Pasted image 20210602191757.png](Pasted%20image%2020210602191757.png)