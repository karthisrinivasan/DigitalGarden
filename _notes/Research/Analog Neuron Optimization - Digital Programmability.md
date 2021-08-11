[[Research]] [[Neuromorphic]]

# Optimizing an Analog Neuron Circuit Design for Nonlinear Function Approximation

[[Research/Kwabena Boahen]] [[Terrence Stewart]]

cf. [[Neural Engineering]]
- Titration of mismatch and digital correction for better distribution of tuning curves (close to uniform)
- ![[Pasted image 20210628152909.png]]

### Silicon Neuron Response Curve
- Spike -> current pulse -> filter (time(synapse) + space(diffusor)) -> spike train
- All processes subject to mismatch
- ![[Pasted image 20210628153044.png]]
#### Pulse-Extender and Synapse
- PE accepts spike, generates current pulse (+/-) 
#### Diffuser
- Emulates current spread in hexagonal resistive network
- Programmable conductances
#### Soma
- Modified Axon-Hillock for relaxation oscillator

### Sizing and Programmable Bias Levels
- ![[Pasted image 20210628161445.png]]
- ![[Pasted image 20210628161147.png]]
- More than 7 levels -> diminishing returns
- 38% area savings
- Improved yield