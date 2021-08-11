[[Research]] [[Neuromorphic]] [[Neuroscience]]

# Legendre Memory Units: Continuous-Time Representation in Recurrent Neural Networks

[[Chris Eliasmith]]

## Memory Cell
- Orthogonalizes time history of its input signal across a sliding window
- Approximate the delay $F(s)=e^{-\theta s}$ by coupled ODEs
- ![[Pasted image 20210710161025.png]]
- ![[Pasted image 20210710161235.png]]

## Characteristics
- Linear-nonlinear trade-off
	- d linear memory units and n non-linear hidden units, backprop to learn coupling
- Parameter-State Trade-offs
	- d,n set independently to trade storage for parameters while balancing linear memory capacity with hidden nonlinear processing

## Spiking Implementation
- ![[Pasted image 20210710161835.png]]

