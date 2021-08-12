[[Research]] [[Neuromorphic]]

# Synaptic Dynamics in Analog VLSI

[[Chiara Bartolozzi]] [[Giacomo Indiveri]]

- Non-impulsive dynamics required for neurons to distinguish different temporal spike patterns, with time constants similar to that of neuron itself

## Synaptic VLSI Circuits
- Fast pulses -> long-lasting currents : subthreshold circuits
- Kinetic models equivalent to DPI

### Pulsed Current-Source Synapse
- Mead, 1989
- VCCS activated by active-low spike
- ![Pasted image 20210610191826.png](Pasted%20image%2020210610191826.png)
- $I_{syn}=I_0e^{-K(V_w-V_{dd})/V_T}$
- Does not integrate into continuous currents
- Timing distribution cannot be discerned

### Reset-and-Discharge Synapse
- Duration of output can be extended
- ![Pasted image 20210610192118.png](Pasted%20image%2020210610192118.png)
- $M_{pre}$ - digital switch
- $M_t$ - subthreshold current source
- $M_{syn}$ - EPSC generation dependent on $V_{syn}$ node
- $I_{syn}=I_0e^{-K(V_{syn}(t)-V_{dd})/V_T}$
- Node reset to $V_{dd}$ after input pulse ends
- For a spike train: $p(t)=\sum\delta(t-t_i)$
	- Response is $I_{w0}e^{(t-t_n)/\tau}$
	- Only depends on last spike
- Non-linear, analysis intractable

### Linear Charge-and-Discharge Synapse
- ![Pasted image 20210610192809.png](Pasted%20image%2020210610192809.png)
- During pulse $V_{syn}$ decreases linearly
- $I_{syn}$ increases exponentially
- In between spikes, $I_{syn}$ decrease exponentially
- ![Pasted image 20210610201333.png](Pasted%20image%2020210610201333.png)
	- spike start and end times
- Response to spike sequence
	- ![Pasted image 20210610201354.png](Pasted%20image%2020210610201354.png)
- Not linear integrator
- Current saturates for high frequencies

### Current-Mirror-Integrator Synapse
- Baohen, 1997
- ![Pasted image 20210610193217.png](Pasted%20image%2020210610193217.png)
- ![Pasted image 20210610201411.png](Pasted%20image%2020210610201411.png)
- sigmoidal increase, 1/t decrease
- Cannot linearly sum PSCs

### Log-Domain Integrator Synapse
- True linear integrator circuit
- ![Pasted image 20210610193651.png](Pasted%20image%2020210610193651.png)
- ![Pasted image 20210610201430.png](Pasted%20image%2020210610201430.png)
- during spike - ![Pasted image 20210610201448.png](Pasted%20image%2020210610201448.png)
- combining with above equation - ![Pasted image 20210610201455.png](Pasted%20image%2020210610201455.png)
	- No dependence on $I_{syn}$ in RHS of equation anymore
- ![Pasted image 20210610201535.png](Pasted%20image%2020210610201535.png)
- More area, microsecond pulses too short to see any effect

## Differential-Pair Integrator Synapse
- Linear, solves problems of log-domain integrator
- ![Pasted image 20210610194119.png](Pasted%20image%2020210610194119.png)
- nFETs - diff pair
- ![Pasted image 20210610201552.png](Pasted%20image%2020210610201552.png)
- ![Pasted image 20210610201608.png](Pasted%20image%2020210610201608.png)
- ![Pasted image 20210610201701.png](Pasted%20image%2020210610201701.png)
- $I_o$ replaced by $I_{gain}$
- Can be used to amplify response amplitude
- Compact layout
- Independent control of time constant, weight, scaling parameters

## Experimental Results
- ![Pasted image 20210610194707.png](Pasted%20image%2020210610194707.png)
- Steady freq. response equation ![Pasted image 20210610201727.png](Pasted%20image%2020210610201727.png)
- ![Pasted image 20210610194829.png](Pasted%20image%2020210610194829.png)
	- Wide linear range

## Synaptic Dynamics
- ![Pasted image 20210610194936.png](Pasted%20image%2020210610194936.png)
- Adding more FETs - NMDA synapse, conductance-based synapse etc.
- Compatible with STDP

### NMDA Synapse
- Voltage gated + ligand gated
- Voltage gating
	- If $V_{mem}$ lower than bias $V_{nmda}$, $I_{syn}$ flows through $M_{nmda}$ and doesn't affect 
	- If $V_{mem}$ higher, current flows into $V_{mem}$ node
- ![Pasted image 20210610195440.png](Pasted%20image%2020210610195440.png)
	- dashed line $V_{nmda}$ threshold

### Conductance-Based Synapse
- Real synapse, current proportional to PS $V_{mem} - E_{ion}$ : ion reverse potential
- ![Pasted image 20210610201849.png](Pasted%20image%2020210610201849.png)
- G block, first order approximation to this
- ![Pasted image 20210610200515.png](Pasted%20image%2020210610200515.png)
- ![Pasted image 20210610202108.png](Pasted%20image%2020210610202108.png), which is approximately:
- ![Pasted image 20210610201939.png](Pasted%20image%2020210610201939.png)
- $V_{gthr}$ ~ $E_{ion}$

### Synaptic Plasticity
- Change of weight - bias $M_w$ in subthreshold with different voltages
- STD with activity, recovery with inactivity
- ![Pasted image 20210610200752.png](Pasted%20image%2020210610200752.png)
	- 50Hz input
- STD block
- Activity-dependent synaptic scaling (homeostasis property)
- Change $I_w$ or $I_{gain}$
- ![Pasted image 20210610201017.png](Pasted%20image%2020210610201017.png)
	- single pulse input
	- Variable response by varying $V_{thr}$ and $V_w$
