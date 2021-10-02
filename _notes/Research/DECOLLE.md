[[Research]] [[Neuromorphic]]

# Synaptic Plasticity Dynamics for Deep Continuous Local Learning

- A spiking neural network equipped with local error functions for online learning with no memory overhead for computing gradients
- Capable of learning deep spatio temporal representations from spikes relying solely on local information
- DECOLLE scales linearly with the number of neurons
- DECOLLE uses surrogate gradients to perform weight updates, but as discussed later, the cost function is local in time and space, such that only one trace per input neuron is required
- DECOLLE can be formulated as a local, three-factor synaptic plasticity rule, and is thus amenable to implementation in dedicated, event-based (neuromorphic) hardware

## DECOLLE
- Random readout at each of the N layers:
	- $Y_i^l=\sum_j G_{ij}^lS_j^l$
	- Fixed random matrices: $G_{ij}^l$
- Global Loss = Sum of layerwise losses
	- $\mathcal{L}=\sum L^l(Y^l)$
- Enforce locality:
	- $\frac{\partial L^l}{\partial W_{ij}^m}=0$ if $m\neq l$
- Weight Updates:
	- $\Delta W_{ij}^l=-\eta \frac{\partial L^l}{\partial S_i^l}\frac{\partial S_i^l}{\partial W_{ij}^l}$
	- $\eta$ -> learning rate
- $\frac{\partial S_i^l}{\partial W_{ij}^l} = \frac{\partial \Theta(U_i^l)}{\partial U_i^l}\frac{\partial U_i^l}{\partial W_{ij}^l}$
	- Vanishes everywhere except zero (spiking nonlinearity
	- Use [[Surrogate Gradient Learning]] to fix
	- Replace $\Theta$ with $\sigma$, a smooth function
	- $\frac{\partial S_i^l}{\partial W_{ij}^l} = \sigma'(U_i^l)\frac{\partial U_i^l}{\partial W_{ij}^l}$
	- Rightmost term calculated from synapse dynamics, ignoring membrane conductance change terms

### Complexity
- O(NT) 
	- T -> no. of timesteps
	- N -> No. of neurons

### Plausibility
- Three factor rule (modulation, pre-syn, post-syn)