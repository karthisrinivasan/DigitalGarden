[[Research]] [[Neuromorphic]]

# Neuromorphic Electronic Systems
- [[Carver Mead]]

- Manipulating single molecules more efficient than using continuum physics (transistors)?
	- Not really, since nerve membranes use populations of channels
	- Transistors rely on single channels being accurate

- Energy disparity
	- Wires cause most of the capacitance
	- >>1 transistors per operation
	- Fix by localizing algorithms
- THree levels
	- Bottom: elementary function
	- middle: representation of info
	- top: organizing principles

### Computation primitives
- Energy barrier
	- difference in dielectric constant between fat and aqueous solution
	- bandgap in transistors
- current is exponential function of barrier energy in nervous tissue
- ![[Pasted image 20210526104559.png]]
- computations implemented using this exp. relation?
- analog memory - charge storage

### Retinal Computation
- Voltage at every point in network is spatially weighted average of photoreceptor inputs
- Each photoreceptor - voltage input to drive node of resistive network
- ![[Pasted image 20210526105129.png]]
	- Pixel schematic
	- conductance of OTA, resistor value - space constant of the network - effective averaging area
	- provide automatic gain control
- Intensity of illumination: $u=f(x,y)$
- Brightness sensation $v$ of the corresponding retinal point:
	- $v=u-m(\frac{d^2u}{dx^2}+\frac{d^2u}{dy^2})$
	- $v$ influenced by local spatial distribution of $u$ too
	- Laplacian filter (difference of Gaussians)
- Retina also sharpens time response - if time scale of external events matches that of computation
	- resistor network cap voltage temporal average too
	- Exponential decay  due to time constant
	- Output of retina is hence difference between immediate local intensity and the spatially+temporally smoothed image

### Adaptive Retina
- Variation in sensitivity, strength of receptors
- Biological retina uses adaptive mechanisms to compensate
- Leakage conductance present during UV illumination - mechanism for adapting charge on floating gate
- Feedback connection from resistor network to photoreceptor
- ![[Pasted image 20210526115816.png]]
	- Correct for output variations with UV light
- Small differences between center intensity and surround intensity converted to large output voltages
- Preserves large dynamic range
- If the output node is high, the floating gate will be charged high, thereby decreasing the current into the output node. If the output node is low, the floating gate will be charged low, thereby increasing the current into the output node. 
- The feedback is thus negative, driving all output nodes toward the same potential.

### Adaptation and Learning
- ![[Pasted image 20210526120951.png]]
- Random walk in case of error
- Truly random events get canceled out
- Systematic differences get learned and adapted to
- Inherent removal of meaningless detail
- Self-organizing system

### Neural Silicon
- Adaptive analog techniques can utilize potential of silicon better than other approaches
- Wafer-level integration 
	- Extremely low power dissipation
	- Adaptive to failure
	- Natural convective cooling sufficient

### Scaling Laws
- Brain - local connections mostly
- 2D case
	- On average, the number of wires decreases at least as fast inverse of length, squared
	- Based on constraint on reasonable total area
- Same law for 3D structures also
- Brain uses folded 2D arrangement
- cf. [[Neocortical Columns]]

