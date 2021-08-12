[[Research]] [[Neuromorphic]] [[MITACS Project]]

# A scalable multi-core architecture with heterogeneous memory structures for Dynamic Neuromorphic Asynchronous Processors (DYNAPs)

- [[Saber Moradi]] [[Giacomo Indiveri]]

- New routing scheme
	- Minimizing memory resources and maximizing programmability/flexibility
- 2-stage 
	- Pont-to-point source addresss touing
	- multiast destination affress touring

## Memory Optimized Routing
- N neurons, F fanout each
- Standard scheme: $log_2(N)$ bit address for a neuron
	- $NFlog_2(N)$ total memory size
- New scheme: Clustering, 2 stage connectivity
- ![Pasted image 20210603182458.png](Pasted%20image%2020210603182458.png)
	- F/M fanout instead of F.
	- N/C intermediate nodes with p2p routing 
		- Broadcasts to all neurons in its target cluster
		- C neurons/cluster
		- F/M<N/C
	- Each target neuron uses one of K tags to determine whether to accept AER packet
- Total source (sender) memory required:
	- (F/M)log(K)+log(N/C)
- Total receiver memory required:
	- (KM/C)log(K)
- Total memory:
	- $Mem = \frac{F}{M}log_2(\alpha N)+\alpha Mlog_2(\alpha C)$
	- Optimal value: $2\sqrt{\alpha Flog_2(\alpha C)log_2(\alpha N)}$
	- Smaller scaling with N, compared to traditional (log(N))

## Mixed-Mode Hierarchical Mesh-Routing Architecture
- 1 cluster -> 'core'
- Intermediate node -> asynchronous router
- tags: stored in content addressable memory (CAM) blocks
- ![Pasted image 20210603184153.png](Pasted%20image%2020210603184153.png)
	- R1: responsible for local traffic
		- Stores source memory in SRAM
	- R2: longer distance, nonlocal traffic
	- R3: high level router

### Quasi Delay-Insensitive Asynchronous Design
- Communicating Hardware Processes (CHP) 
- Handshaking Expansion (HSE) formalism
- No assumption on gate delays, only propagation delays
- CHP -> HSE -> low-level circuit description
- Controlled-pass process
	- inputs: 
		- in - holds date
		- sig - control bit whether or not to copy to out
			- dual rail representation (sig.t, sig.f)
	- outputs: out
	- ![Pasted image 20210605122140.png](Pasted%20image%2020210605122140.png)
	- ![Pasted image 20210605122202.png](Pasted%20image%2020210605122202.png)

### Asynchronous Routing Fabric
- 256 neurons/core
- 3 cores/tile
- R1 router - 1 per core
	- Bidirectional link between R1<->local core, R1<->R2
	- ![Pasted image 20210605122635.png](Pasted%20image%2020210605122635.png)
- R2 router - inter-tile communication
	- ![Pasted image 20210605122920.png](Pasted%20image%2020210605122920.png)
- R3 router
	- XY routing - decrement till zero along both axes to determine destination
	- ![Pasted image 20210605123009.png](Pasted%20image%2020210605123009.png)

- Input Interface
	- Send stimuli to neurons from external sources
	- Program SRAM and CAM
	- Configure biases
	- ![Pasted image 20210605123155.png](Pasted%20image%2020210605123155.png)
- 


## Multi-Core Neuromorphic Processor
- 4x256 analog AdExp-I&F neurons
- Sub-threshold DPI log-domain synapse
	- ESPC,IPSC time constant range: ~1us - ~100ms
- ![Pasted image 20210603190023.png](Pasted%20image%2020210603190023.png)

### Core Memory/Computing Module
- ![Pasted image 20210603190231.png](Pasted%20image%2020210603190231.png)
- Dedicated DPI circuit for each behavior
	- fast exc.
	- slow exc.
	- subtractive inh.
	- shunting inh.
- 
### Asynchronous CAM Circuits
- ![Pasted image 20210603190334.png](Pasted%20image%2020210603190334.png)
- Does not use QDI
- cf. [[Thesis - Syutkin, Anatoly#Content Addressable Memory]]

## Experimental Results
- Overall performance limited by I/O circuit speed
- ![Pasted image 20210605124432.png](Pasted%20image%2020210605124432.png)
- Broadcast time of CAM also limiting (27ns here)
- ![Pasted image 20210605124537.png](Pasted%20image%2020210605124537.png)
- ![Pasted image 20210605124616.png](Pasted%20image%2020210605124616.png)
- Allows 7200 fan-in per neuron at 20Hz mean firing rate

### CNN Card Suit Recognition
- ![Pasted image 20210605125140.png](Pasted%20image%2020210605125140.png)
	- Frame - aggregate output
	- Number - Firing rate 
- Prediction determined by most active group (4 groups of 64 each, 1 per suit)
- ~30ms classification time
- 100% performance with 2560 neurons
- TrueNorth - quadratic scaling between number of cores and number of neurons
	- Additional cores required for implementing fan-out
- Proposed architecture - linear scaling
	- No additional routing cores needed
- ![Pasted image 20210605125644.png](Pasted%20image%2020210605125644.png)

## Discussion
- Distributed computing systems
	- Price - routing overhead
- Optimal trade-off between network configuration flexibility and routing memory demands

