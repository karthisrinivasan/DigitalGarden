[[Research]] [[Neuromorphic]]

# A Contrast Sensitive Silicon Retina with Reciprocal Synapses
[[Kwabena Boahen]] [[Andreas Andreou]]

## Introduction
- Cones' membrane potentials -> sensitive to ratio between spatial and temporal averages (contrast)
- This work -> first to include variable inter-receptor coupling
- Single transistor gap junction
- ![Pasted image 20210729122121.png](Pasted%20image%2020210729122121.png)

## Retina
- Light on cone -> activity increases -> excites adjacent horizontal cells -> inhibit back
- Excitation from nearby cones stronger than inhibition from horizontal cells
- cf. [[Dynamic Field Theory]]
- ![Pasted image 20210729122415.png](Pasted%20image%2020210729122415.png)
	- Cone membrane potential
	- Conductances proportional number of open channels

## Silicon Models
- Subthreshold MOSFET -> gap junction (diffusion current)
- Gate voltage sets the diffusivity
- 5 decade dynamic range
- Current mode diffusor
- ![Pasted image 20210729122949.png](Pasted%20image%2020210729122949.png)	
	- Currents in M1,M2 proportional to carrier concentration at ends of M3
	- Hence diffusor current proportional to difference between M1 M2 currents
	- ![Pasted image 20210729123114.png](Pasted%20image%2020210729123114.png)
- Chemical synapse -> MOSFET in saturation
	- VCCS behavior
- Modulating gap diffusivity -> inhibition emulation
- 1D retina model
	- ![Pasted image 20210729123930.png](Pasted%20image%2020210729123930.png)
	- M1 M2 -> reciprocal synapses
	- M4 M5 -> gap junctions
	- M6 -> light sensitive input
	- M3 -> leak and balances input
- Operation
	- IC IH -> cone, horizontal cell responses
	- VC VH -> log of response 
	- current increases -> VC drops, M2 on, IC increases (excitation)
	- IC pulls VH down, M1 on, IH increases (excitation)
	- IH pulls VC up M2 off, IC decreases -> inhibition
	- similar to diffusor circuit
		- reference voltage depends on h cell response

## Relation to Linear Models
- Biharmonic equation to find optimally smooth interpolating function IH for noisy discrete data I
	- ![Pasted image 20210729124857.png](Pasted%20image%2020210729124857.png)
	- Solve for IH from: ![Pasted image 20210729125054.png](Pasted%20image%2020210729125054.png)
- Horizontal cell -> compute smoothed version of image
- cones -> edge detection by taking Laplacian
-