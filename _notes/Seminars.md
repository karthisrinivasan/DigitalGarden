[[Research]] 
---
## Low Power Voice-Activity Detector 
[[Analog]] 
- Low latency and low SNR operation required
- Prior art
	- High latency (100ms)
	- Hit Rate ~85%
- Proposed
	- BPF+Rectifier followed by 2-layer Analog NN
	- No need of LPF at the end
	- Multi-layer ternary (-1,0,1) network
	- Low power (28.5uW)
	- Works at ~0dB SNR too
	- 10ms latency

## High-Resolution DSM Design Techniques
- ISI determined by NMOS PMOS matching
	- causes HD2
- Reference path resistance - causes HD3
- Distortion eliminated using dummy DAC
	- injects charge whenever main DAC doesn't
	- injection now data-independent
- CMFB prevents distortion due to diff ip imbalance
- Chopping mitigation
	- 3-stage OTA + FIR feedback
	- Improves in-band noise
- 10ps jitter tolerance
- >100dB SNDR w 250kHz BW


## NeuroTech Day 8
- Marcel Strimberg, Thomas Nowotny

### NEST
-	Hans Plesser - Norwegian University of Life Sciences
-	HBP, EBRAINS

### BRIAN
- Marcel Stimberg - Institut de la Vision
- Standalone mode (as opposed to runtime mode)
	- Faster for longer runtimes, smaller networks
	- Complete C++ project
	- Less flexible <- no python interaction during run
- No meaningful parallelization

### GeNN
- Thomas Nowotny, University of Sussex

## Neurotech - Algorithms 

###  Problems with Online Learning
- Memory time scales
- Benna, Fusi 2016

### Levels of Neuromorphic Computing
- Offline
- In-the-loop learning (PC+Chip)
- On-chip only
- TTFS coding - fingertip angular pressure

### Online Learning in Practice
- Local loss functions
- Direct Feedback Alignment
- MAML with SG

### Reservoir Computing
- Locality
- Simplicity
- Online
- Does not interfere with reservoir dynamics
- Learning restricted to one layer



