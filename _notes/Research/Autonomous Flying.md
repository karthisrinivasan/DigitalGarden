[[Research]]
# Autonomous Flying With Neuromorphic Sensing
- [[perspective]] [[Neuromorphic]] 
## Introduction
- Current airplanes generate huge amounts of data (~3TB per day per plane)
- In contrast, birds have much simpler sensor networks

## Missions and Needs
- Capabilities to achieve autonomous fight - attitude control, collision avoidance, height control, navigation
- combo of centralized and distributed sensors
- hyperspectral imaging
- learn and act upon sensory inputs

## Current Advances in Neuromorphic Sensing
- Event-based detection
	- deviations from value
- [SNN chip for radar signal processing](https://www.imec-int.com/en/articles/imec-builds-world-s-first-spiking-neural-network-based-chip-for-radar-signal-processing)
- Desire to reduce latency, improve energy efficiency, dynamic range and sensitivity
- Limitations
	- handling high focal plane array utilization

## Bio-Inspiration
- Active models
	- echolocation in bats
- Spatial attention
	- allocation of resources to relevant information
	- sharpening of midbrain neurons (encode egocentric coords) and hippocampal place cells (encode allocentric coords)
- Adaptive processing not done in sonar yet
- barn owls
	- low light environments
	- stimulus selection processes
	- competing stimuli
- isnect brains
	- complexity limited
	- still perform complex tasks
- drosophila melanogaster - fruit fly
	- poor spatial resolution
	- optical flow processing

## Outlook - Advancing Neuromorphic Applications
- [[Optical Flow - Loihi - MAVs]]
- DVS in parallel with conventional systems to detect threats earlier
- Larger aircraft - improve sensing using prediction
- Local computing via neuromorphic architectures
- How to fuse active and passive sensors?
	- active challenged by env. objects
	- passive energetically expensive
- Top-down (internal guidance - mission driven) and bottom-up attention (externally driven)
- Predictive coding - updates internal representation of the environment
	- Attention required only when prediction error occurs
- ![Pasted image 20210514130033.png](Pasted%20image%2020210514130033.png)
- Need to enhance understanding of neurosensory systems in flying creatures

![Pasted image 20210514130246.png](Pasted%20image%2020210514130246.png)

## Recommendations
1. Develop event-based sensor hardware and algorithms to support navigation and collision avoidance
2. Develop efficient flight control with fast sensor-to-actuator responses
3. Develop attentional, sensory fusion, and representational mechanisms to increase performance in complex scenarios
4. Develop neuromorphic approaches to learning for adaptive and predictive sensing and control
5. Develop principles to integrate neuromorphic and convolutional approaches