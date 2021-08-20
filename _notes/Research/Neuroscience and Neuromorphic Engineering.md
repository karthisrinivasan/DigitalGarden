[[Research]]

# Visualizing a joint future of neuroscience and neuromorphic engineering
[[Friedemann Zenke]] [[Emre Neftci]] [[Dan Goodman]]

## Introduction
- Contradiction:
	- Spiking models accurately model biology but hard to build complex networks
	- Deep learning models unlike brain but can solve complex problems
- Credit assignment problem
	- Knowing how individual neurons deep inside the network affect output
	- This is required to find right connections
- Solving CAP using gradient based methods is what makes it superior
	- Fails in SNNs due to non-differentiable nature 
- ![Pasted image 20210820122301.png](Pasted%20image%2020210820122301.png)
- Recent innovations combine plausible models with performance-optimized networks
- New models:
	- Take advantage of temporal spiking dynamics to efficiently encode and process information
	- Embrace the computational value of neuronal heterogeneity and multi-time-scale dynamics by jointly optimizing neuronal parameters with the connectivity
	- Learn through biologically plausible learning rules derived from a normative gradient-based framework, providing new vistas on their mechanistic underpinnings at the micro-circuit level.

## Temporal Dynamics
- Temporal coding strategies explored
- Earlier, only average rates were considered
- New ways to translate gradient-based learning to fine-grained temporal spiking
	- [[Surrogate Gradient Learning]]
	- Similar to cortical processing
	- More efficient on hardware
	- Sparse but precisely timed spikes
	- Gradients with respect to single spike times

## Time-Continuous Processing with Instantaneous Rates
- [[FORCE Training Algorithm]]
- Solve regression over linear combinations of filtered spike trains at every instant while using PSP as kernel
- Does not require stationary firing rates
- Solves complex sequence generation problems
- Robust to choice of neuron model

## Efficient Low-Latency Processing with single spikes
- Each neuron spikes once in given time period
	- Assumes extreme sparseness
- SOTA accuracy
- Provides universal approximators
- Robust to manufacturing imperfections
- Useful for processing static stimuli using latency codes
- Not very useful for temporal stimuli
	- Can be overcome via surrogate gradients

## Coordinated Neuronal Heterogeneity
- Networks where surrogate gradient learning can optimize time constants and and other neuron/synapse parameters
	- Demonstrated improvements
- Lots of potential for research

## Multi-Timescale Dynamics
- Dynamical complexity of neurons important in shaping computation
- Moving thresholds improves performance drastically wrt fixed
- Spike frequency adaptation also leads to reduction in spike counts and thereby energy consumption

## Normative and Plausible Plasticity Models
- Gradient based algorithms not plausible
	- Hence does not provide biological insight
- Memory requirements grow with stimulus duration
- Real-time recurrent learning (RTRL) only requires forward propagation of information
	- Still requires non-local information
- Deep continuous local learning (DECOLLE) most plausible as of now
	- Synaptic eligibility traces fall out of this framework

## Plausible Solutions to CAP
- Eligibility traces -> starting point for temporal CAP (which past network activity contributed to a specific error or reinforcement signal later in time)
- Spatial CAP (which neuron’s activity contributes strongly to a particular network-level output) requires dedicated circuits
	- Brain's solution is an open question
- Precisely times learning signals to a population have been proposed
	- Mechanism unknown
- Burst multiplexing
	- Isolated spikes have different meaning than HF bursts
	- Two separate information channels over same physical channel
	- Demonstrated competitive performance on large-scale tasks like ImageNet

## Future Challenges
### Conceptual
- Quantitative ways of comparing network representations across networks
- Temporal structure of spike trains may require new analysis techniques
- Incremental moves toward plausibility by incorporating biological constraints
- Detailed knowledge about brain's input encoding is needed to improve SNNs
### Technical
- Size limitations on large simulations
- Need architectures tailored to sparse networks
- Need plausible spike datasets
- Which tasks are SNNs better for?

## Big Question
- Why spikes?