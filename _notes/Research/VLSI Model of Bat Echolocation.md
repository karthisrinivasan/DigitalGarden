[[Research]] [[Neuromorphic]]
# A Neuromorphic VLSI Model of Bat Interaural Level Difference Processing for Azimuthal Echolocation
- [[Timothy Horiuchi]]

## Introduction
- Little known about computation for echolocation in air
- Echo delay - distance
- Echo amplitude and spectrum - geometry
- Two ears for direction determination
- Interaural Time Difference (ITD) and Interaural Level Difference (ILD)
- Larger animals use ITD and ILD, bats largely dependent on ILD only
- High frequency <-> short range
- Short pulse => 1 or 2 spikes per echo => representational challenge
- Timing code likely
- Modular VLSI implementation

## Biology and System Model
### Azimuthal Echolocation Cues
- Sound Pressure Level (SPL):
	- $SPL=20log_{10}\frac{p_{rms}}{p_{ref}}$
- Difference in SPL => ILD (also known as IID, interaural intensity difference)
- Defined as difference between excitatory and inhibitory stimulus here
-  $ILD=20log_{10}\frac{p_{rms,e}}{p_{rms,i}}$
![[Pasted image 20210530104624.png]]
- ILD at multiple frequencies combined for unique pattern
- Small head => max ITD is very small
	- Cannot be used effectively

### Processing
- Main unit - EI Cell
	- Receives excitatory input from one ear, inhibitory from other
	- Subtraction when coded logarithmically
- ILD functions for Lateral Superior Olive (LSO) and Inferior Colliculus (IC) neurons
	- ![[Pasted image 20210530105324.png]]
	- Smallest ILD for complete inhibition: $ILD_{ci}$ (*)

### System Model
- Function Diagram:
- ![[Pasted image 20210530105516.png]]
- Abstract model:
- ![[Pasted image 20210530105629.png]]
- Emphasizes role of spike latency in ILD processing using short stimuli
- 3 Layer network interconnected with AER interface for communication

## Sonar Front-End Design
- 40kHz narrow band ultrasonic transducers
- ![[Pasted image 20210530113627.png]]
- ![[Pasted image 20210530113648.png]]
	- ILD as function of source azimuth

### Front-End System
- ![[Pasted image 20210530113844.png]]
- Opamp based circuit - generates spiking input to ILD network

### Envelope Extraction
- Logarithmic amplifier
- Demodulates AM signal and outputs logarithm of envelope
-  $u_o=20log_{10}\frac{u_{in}}{0.02}$
-  45dB linearity

### AVCN Neuron
- Spike generator with high rate
- ![[Pasted image 20210530114958.png]]
- One-shot circuit to generate constant width pulse
- Spike time:
	- $t_{n+1}=t_n+\frac{RCv}{A\bar{u}(t_n,t_{n+1})}$
	- $\bar{u}$: Average value in that interval
- Spike intervals inversely proportional to instantaneous intensity of envelope
- Parameters can be tuned for a desired total spike number:
	- $N=floor(\frac{AU_mT}{RCv})$
	- $U_m=\int_0^Tu(t)dt$
- Biological consideration: N represents total no of synapses x spike per synapse
- ~10 excitatory and 8 inhibitory synapses / LSO cell
- Larger N better for accuracy but need enough time for reset to ensure linear summation of spikes
- Response of AVCN Neuron to 40kHz sine wave pulse (2ms duration)
	- ![[Pasted image 20210530120024.png]]

### Response to Targets
- ![[Pasted image 20210530120134.png]]
- ![[Pasted image 20210530120216.png]]

## Chip Design
### Multilayer Network Chip
- Maximum combinations of ILD processing interconnections
- Should work for different input sources
- ![[Pasted image 20210530120413.png]]
	- Lower half - Layers 1,2
	- Off-chip AVCN circuits provide input 
	- Each  layer - 17 EI cells
	- Each address-> 2 synapses in layer 3 L,R
	- Upper box - layer 3
- Should allow to be reconfigured bu external circuitry
- AVCN - LSO connections
	- ![[Pasted image 20210530120759.png]]
	- +: Variable weights (only for excitatory)

### EI Cell
- Lazzaro-Wawrznyek synapse
- ![[Pasted image 20210530121115.png]]
	- a) excitatory b) inhibitory
- Exponential decay below threshold
- LIF neuron with constant leakage and adjustable refractory period
- ![[Pasted image 20210530121351.png]]
	- C3, M10 - membrane capacitance and constant leak
	- C4, M11-15 - spike generator
	- C5, M19-26 - reset and refractory control
	- M16-18 - request signals for AER

##  Circuit Model and Analysis
### LSO
- One excitatory (E) and one inhibitory (I) input
- $v_m(t)=(aE-bI)t/T$
	- $a$: increase per excitatory spike
	- $b$: decrease per inhibitory spike
- Threshold: $\theta$
- Time to first spike:
	- $t_{spk}=\frac{\theta T}{(a+b/2)ILD + (a-b)ABL}$
	- $ILD = E-I$
	- $ABL = \frac{E+I}{2}$: Average binaural level
- ![[Pasted image 20210530123054.png]]
- Linear subtraction an approximation to staircase here
- ![[Pasted image 20210530123304.png]]
	- Time to first spike vs. ILD
### EI Cells
- Consider cell with single excitatory and single inhibitory spike
- Inhibitory spike can suppress/delay output spike
- ![[Pasted image 20210530125317.png]]
- Two IC cells with different parameters:
	- ![[Pasted image 20210530125429.png]]
	- ![[Pasted image 20210530125444.png]]

## Experimental Results
### Copy Cell and Population
- DNLL and IC neurons inherit properties from LSO -> copy network
	- ![[Pasted image 20210530155424.png]]
- Population response in one chip
	- ![[Pasted image 20210530155548.png]]
	- DIstribution achieved even when all parameters for 16 cells same -> transistor variation
- ILD tuning curve of 3 nominal cells
	- ![[Pasted image 20210530155655.png]]

### EI/F Cell
- Facilitated EI (EI/F) Cell - spatially selective cells in IC
- ~30% of all EI Cells
- ![[Pasted image 20210530160015.png]]
- Test result from sample cell: 40kHz AM bursts
	- ![[Pasted image 20210530160110.png]]

### Real Target
- ![[Pasted image 20210530160245.png]]
- Black: >10 responses (20 trials)
- Different pattern at each point
- Selective azimuth range
- All cells had same configuration but not all responded
- Raster of spike times
	- ![[Pasted image 20210530160540.png]]

### Discussion
- Mismatch produces diversity of response
- Measurements on EI cells from both sides of the brain are necessary to understand ILD processing
- Copy cell copies $ILD_{ci}$ AND spike transforms spike latency 
- EI/F cells respond  maximally around midline
- How is azimuth (and space in general) coded in the brain?
- How is hyperacuity achieved by coarse tuning?