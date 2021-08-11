[[Research]] [[Neuromorphic]]  [[MITACS Project]]
# Loihi -  Neuromorphic Processor with On-Chip Learning
- [[Mike Davies]]

Support for local information for programmable synaptic learning process
-	Spike traces with configurable time constants
-	Multiple traces for a given train filtered with different time constants
-	Two additional state variables per synapse
-	Reward traces for reward/punishment signals for reinforcement learning

Other primitives
- Stochastic noise for neural/synaptic variables
- Configurable delays 
- Configurable dendritic tree processing
- Neuron threshold adaptation
- Scaling and saturation of synaptic weights

## Architecture
- 128 neuromorphic cores
- 3 x86 cores
- Asynchronous NoC system for transport within cores
- 1,024 neurons per core
- Additional features
	- Sparse network compression
	- Core-to-core multicast
	- Variable synaptic format
	- Population-based hierarchical connectivity

### Mesh Operation
- ![[Pasted image 20210607163634.png]]

### Network Connectivity
- ![[Pasted image 20210607164008.png]]
- Directed multigraph structure

## Design Implementation
- ![[Pasted image 20210607182129.png]]

### Asynchronous Design
- ![[Pasted image 20210607182628.png]]

## Results
- ![[Pasted image 20210607182853.png]]
- ![[Pasted image 20210607182953.png]]