[[Research]] [[Neuroscience]] [[Neuromorphic]] [[MITACS Project]]

# A Two-variable Silicon Neuron Circuit based on the Izhikevich Model

[[Nobuyuki Mizoguchi]]

- cf. [[Izhikevich Model]]

## Designed Circuit
- ![[Pasted image 20210621110918.png]]

### Reproducing nullclines
- ![[Pasted image 20210621111047.png]]
	- v nullcline
	- bump-antibump circuit
- ![[Pasted image 20210621111059.png]]
	- u nullcline
- ![[Pasted image 20210621111534.png]]
	- dynamics of u
	- current integrator
	- subthreshold
	- $\frac{dI_{out}}{dt}=\frac{I_{\tau}}{CU_T}(I_{in}-I_{out})$
	- $I_{\tau}$ <-> a (Izhikevich model)

### Reset Circuit
- ![[Pasted image 20210621113612.png]]

### U+D Circuit
- ![[Pasted image 20210621113626.png]]
- Iout1 / 2 <-> +/- d

## Results
- 0.35um TSMC 
- +/- 1.65V supply
- 17/20 Izhikevich patterns


