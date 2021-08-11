# Loihi - Survey of Results and Outlook
- [[Mike Davies]]
[[Research]] [[Neuromorphic]] 
## Introduction
- fully integrated memory-and-computing
- fine-grain parallelism
- pervasive feedback and recurrence
- massive network fan-outs
-  low precision and stochastic computation
-  continuously adaptive processes	
-  TrueNorth: digital neuromorphic but high energy efficiency

## Loihi, Systems and Software
### Loihi Chip
- 130k LIF neurons - digital discrete time model
- 128 cores
- comm thru spikes
- variable weight precision
- Bi-and-Poo STDP rule and others
- Barrier messages - synchronizing spikes
	- handshaking for deterministic operation
- 3 x86 cores
	- data format conversion

### Systems
- Commercial - standard interfaces on-chip
- Kapoho Bay, Nahuku, Pohoiki Springs

### Software
- NxSDK
	- snips - sequential neural interfacing processes
	- interact with neurons, real-time data conversion, sequencing operations, configuring neuron params
- Various levels of abstraction - neuron, network, function

## DL for SNNs
- Synaptic op simpler than multiply-and-accumulate
- SNNs don't outperform ANNs on hardware optimized for ANNs obviously
- Algorithms: online, offline
	- online: deploy to hardware, train in real time
	- offline: deploy trained model
- Performance with respect to Loihi
- Metric: Energy Delay Product (diag line = const)
- ![[Pasted image 20210507093222.png]]

### Deep DNN Conversion
- Near lossless
- Matching of behavior according spike-based info encoding model
- ANN activation -> firing rate in SNN
- more bits -> exponentially more enc time

### Direct Deep SNN Training
- Back-propagation to optimize SNN params
- spike gen fn - ANN nonlineairty
- DVS data
- timing code -> energy+info efficient, lower latency
- SNN -> model as recurrent ANN for training
- spike fn - inf derivative
	- surrogate fn - errors as net scales
- SLAYER Spike Layer Error Reassignment, STDB spatio-temporal back-propagation
- Better than conversion

### Online Approx. of Back-propagation
- Expensive 
- Under development

## Attractor Networks
- Brain - emergent computation	
- Nonlinear Dynamical Systems
- Attractor dynamics: simple collective dynamics for nontrivial computation
	- Convergence guarantee: Lyapunov condition

### Locally Competitive Algorithm (LCA)
- Feature neurons - mutually inhibited with recurrent connections
- balance between feedforward input and recurrent inhibition  -> competition
- Equivalent to LASSO 
- ![[Pasted image 20210507102137.png]]
- Sparse coding - protection from adversarial images
- LCA - first processing layer in neuromorphic pipeline
- Dictionary learning - online, unsupervised

### [[Dynamic Neural Fields]]
- Attractor states -> Behavioral attractors
	- location/velocity
- Most strongly stimulated state(s) manifest as persistent activation
- Local excitatory connections stabilize manifold structure
- Model cognitive brain processes that require working memory
- High computational cost
- Stable states counter analog variability
- Tracking DVS object on Loihi
	- 64x64 grid; 240x180 input field

## Computing with Time
- Need to go past converting ANN models

### Nearest Neighbor Search
- Cosine distance
- Each datapoint - input weights of one neuron
- PCA/ICA for preprocessing - dimensionality reduction
- Comparable accuracy to state-of-the-art

### Graph Search
- Hippocampus spike wavefronts - shortest route finding
- Graph - physical core
- Edge - Two-way edge in Loihi map
- Destination node excited - wavefront propagates through to source node
- Spike passage - zeroing of weights to highlight path
- Each neuron responds to wavefront only once
- Non-path neuron would have both weights zeroed, path neuron would have only side 
- Read path of non-zero weights to find path
- O($nd\sqrt{E}$)
	- n: no. of edges
	- d: average edge cost
	- E: proportional to no. of edges and nodes
- ![[Pasted image 20210507194925.png]]

### Stochastic Constrained Optimization
- Solve NP-complete constraint satisfaction problems
- Latin Square Problem
	- NxN array off variables
	- Each can take on N possible values 
	- No repetition in row/column
- WTAs - individual variables
- All-different constraint - inhibitory connections
- Pruning through firing until only non-conflicting neurons are active
- ![[Pasted image 20210507201051.png]]
- Loihi faster, more efficient
- 1000x smaller EDP
- Incomplete solver, of course
- Found optimal solutions for all test cases so far, though
- Incremental solving - time-critical applications

## Applications
- Event-Based Sensing and Perception
- Odor Recognition and Learning
	- Outperforms conventional algorithms by over 40% (accuracy)
	- Imam and Cleland, 
	- No forgetting
- Closed Loop Control for Robotics
	- Hough transform on SNN
	- Gait generation using oscillatory networks
- SLAM
- Dynamic RF waveform adaptation
- Heat diffusion equation solver

## Outlook
- Deep Networks
	- Energy efficiency at the cost of latency
	- Relay cores/multicast interchip links
- Online Learning
	- Difficult to do actual real-time learning
	- Shallow learning?
- Sensor Integration
	- More DVS-type sensors and integration needed to unlock full potential
- Robotics
	- Go beyond classical control theory
- Planning, Optimization, Reasoning
	- Vector symbolic architectures (VSAs)
	- Knowledge representation
	- Interfaced with DNs - maybe path to next-gen AI on neuromorphic hardware
	- Spike-based Phasor associative memory network ([[TPAM]])
- Programming Framework
	- Nengo - built around NEF
- Economic Viability
	- Expensive logic state bits
	- Cheap integration of memory devices (RRAM, PCM etc.)

![[Pasted image 20210507203329.png]]
