[[Research]][[Neuromorphic]]
# Enabling Resource-Aware Mapping of Spiking Neural Networks via Spatial Decomposition
[[Jeffrey Krichmar]]

### Introduction
- How to efficiently use crossbars when not all neurons have the same number of input synapses
- Unrolling technique 
	- Decompose neurons into homogeneous neural units where each has max fanin of two (FIT)
- Denser packing per crossbar

### Proposed Technique
- ![[Pasted image 20210529114749.png]]
- Pruning - elimination of near-zero weights
- Unrolling - limit number of presynaptic connections
- Weight normalization - ensures quality of decomposed model

#### Spatial Decomposition using Model Unrolling
- 1 m-input neuron -> (m-1) 2-input neurons
- ![[Pasted image 20210529115055.png]]
- $y_0=f(u_{m-1})$
- $u_i:$
	- $f(n_1.w_1+n_2.w_2) for$ $i=1$
	- $f(u_{1-1}+n_{i+1}.w_{i+1})$ $otherwise$
- $f$: neuron function
- total number of FIT neurons from N-neuron network:
	- $N_{new}=\sum_1^N(m_i-1)$
	- $m_i$ - fanin of neuron $n_i$

#### Weight Normalization
- Weights normalized such that the firing rate of new neuron is proportional to its input activation in original model
- Performed separately for each decomposed unit
- $w_i=$
	- $w_i/S^1_{norm}$ for i=1,2
	- $w_i/S^{i-1}_{norm}$ otherwise
- $S^i_{norm}=$
	- $k(max(a_1+a_2)$ for i=1
	- $k(max(a_{i+1})$ otherwise
- $a_i$ activation on weight $w_i$ in the original model
- Overhead can be reduced by allowing non=uniform decomposition

#### Motivating Example
- Mapping of functions onto 4x4 crossbar
- ![[Pasted image 20210529120928.png]]
- Last term of $y_2$ cannot be mapped, normally
- Unrolling enables mapping
- Fewer crossbars, no loss in model quality, increase in crossbar utilization

### Results

- ML Applications used:
	- ![[Pasted image 20210529121317.png]]
- Evaluated on [[DYNAP-SE]] (128x128 crossbar per tile):
	- ![[Pasted image 20210529121350.png]]

- Comparison of Hardware Requirement
	- ![[Pasted image 20210529121422.png]]
	- 60% fewer crossbars on average
	- 10x fewer crossbars in EdgeDet even though EdgeDet has no neurons with more than 128 fanin
		- Due to many having close to 128
		- Hence many instances of 1 crossbar/neuron
	- CNNs - more layers => more freedom to improve crossbar utilization
	- RNNs - Cyclic connections decomposed effectively

- Comparison of Crossbar Utilization
	- Neurons: 53% vs. 9% average utilization
	- ![[Pasted image 20210529121856.png]]
	- Synapses: 62% vs. 25% average utilization
	- ![[Pasted image 20210529121913.png]]

- Comparison of Wasted Energy
	- Incorporates neurons and synapses that are not utilized during execution
	- 62% lower energy usage on average
	- ![[Pasted image 20210529122143.png]]

- Comparison of Model Quality
	- Same in some cases due to some models having strictly <128 synapses/neuron
	- 3% better on average for networks that don't satisfy this constraint
	- ![[Pasted image 20210529122317.png]]

### Discussion
- Negative impact on accuracy and energy
- Spike latency affected due to unrolling
	- Alleviated by SpiNeMap somewhat
- Additional synapses mapped to shared interconnect
	- Energy on interconnect increases
	- Much lower compared to energy savings gained

