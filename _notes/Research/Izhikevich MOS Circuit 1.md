[[Research]] [[Neuroscience]] [[Neuromorphic]] [[MITACS Project]]

# An Izhikevich Model Neuron MOS Circuit for Low Voltage Operation

[[Yuki Tamura]]

- cf. [[Izhikevich Model]]
- Redesigned sub-circuits
- Lower voltage supply

## Proposed Circuit
- ![[Pasted image 20210602202734.png]]
- V sub-circuit:
	- ![[Pasted image 20210602202922.png]]
	- Removes unnecessary $u^2$ term in original circuit, in equation of $v$
- U sub-circuit
	- ![[Pasted image 20210602202932.png]]
	- Cannot reproduce Izhikevich model for negative b

## Experimental Results
- Null-cline closer to model than original circuit
- ![[Pasted image 20210602203236.png]]

### SPICE Simulations
- Parameter ranges for each type of behavior enlarged in new circuit
- ![[Pasted image 20210602203513.png]]
	- a) Original b) New circuit
- ![[Pasted image 20210602203534.png]]

- ~20uW power consumption
- Difficulty in large-scale integration
- Subthreshold designs - future work