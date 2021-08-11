[[Research]] [[Neuromorphic]]
# A Neuromorph's Prospectus
- [[Kwabena Boahen]]
[Research](Research.md)
### Introduction
- Energy efficiency of using multiple low-quality channels
- ![[Pasted image 20210522195214.png]]
- ![[Pasted image 20210522195547.png]]

Five point plan
- Implement computation with sub-threshold analog circuits 
- Implement communication with asynchronous digital circuits
- Distribute computation over pool of silicon neurons
- Communicate spikes between pools with O(n) time complexity; n -> no. of neurons
- Encode continuous signals in spike trains

### Neurogrid
- Address event bus
	- Share wires among population of neurons
	- Has reached limit due to quadratic scaling
- Interconnect problem solved using:
	- Overlapping dendritic trees
	- Hierarchical axonal arbors
	- Thousands of synaptic connections per neuron
- Map cortical area onto group of Neurocores spanned by sub-tree of interchip-routing network
- Columnar organization: [[Neocortical Columns]]
- 1 million neurons, 1 billion synapses
- ![[Pasted image 20210522224329.png]]

#### Overlapping Dendrites and Hierarchical Axons
- Overlapping dendritic trees extend branches to meet incoming axons, instead of axons branching out
- Emulated using crossbar
- ![[Pasted image 20210522224655.png]]
- Hierarchical axonal arbors minimize wiring by replacing n long branches by 1 long branch terminated by n short branches
- Emulated by tree-like routing network
- ![[Pasted image 20210522224843.png]]

#### Neural Engineering Framework
- Spike trains encode vector of $D$ continuous signals
- Transformations of this vector ($f$) linearly decoded from spiking rates $a_i$
	- Spike rates weighted by $D$-dimensional decoding vectors ($d_i$) and summed
- Equivalent to conventional NN with weights
	- $w_{ij}=e_j^Td_i$
- $2ND$ components vs. $N^2$ weights 

### Performing Arbitrary Computations
- Uses [[Neural Engineering]] Framework
- Non-programmable tuning curves
	- Not required in NEF though
- Programmable connections
- Heterogeneous population
- ![[Pasted image 20210522225658.png]]

First NEF-based spiking neuron model brain: Spaun
![[Pasted image 20210522231114.png]]
![[Pasted image 20210522231222.png]]

### Efficient Spike Coding
- Coordinated spiking codes
	- Scale precision linearly with spike rate
- ![[Pasted image 20210522231531.png]]

#### [[Coordinated Spiking Network]]
- Difference wrt NEF network
	- Cell body's contribution to dendrite signal chosen randomly
	- Fraction of dendrite's signal delivered to cell body is chosen deterministically
- ![[Pasted image 20210522232116.png]]

