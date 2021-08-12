# Telluride Neuromorphic Workshop 2021

[[Research]] [[Neuromorphic]]

[Schedule](https://sites.google.com/view/tellurideneuromorphic2021/schedule)

[Zoom](https://us02web.zoom.us/j/82784128779?pwd=bWFkdnc1TExaWTZVbzVJZGxDOHJqZz09)


DVS
![Pasted image 20210628210942.png](Pasted%20image%2020210628210942.png)

Non-volatile Memory Tech.
![Pasted image 20210628212656.png](Pasted%20image%2020210628212656.png)

ANT
- SNN Simulations
- CMOS Design

NMC
- NeuroDyn hardware platform
- Regulation of an automaton
- ![Pasted image 20210628215927.png](Pasted%20image%2020210628215927.png)

SMI
- Closed loop control task 
- Mapping to DVS+Loihi

TAC
- Braille recognition
- Edge following and shape recognition
- Resistive sensing circuit design

TAD (Discussions)
- Ethics and Social Justice in Neuromorphics
- ![Pasted image 20210628225359.png](Pasted%20image%2020210628225359.png)

Nengo

## Neurorobotics - Jeff Krichmar
- Morphological computation - by body, to alleviate load on brain
- Degeneracy
- Actions and Reactions
	- Short term plasticity
	- Behavioral repertoires
- Adaptive Behavior
	- Learning and Memory
	- Value and Prediction
- Behavioral tradeoffs
	- ![Pasted image 20210629204835.png](Pasted%20image%2020210629204835.png)

## Tactomorphics - Nitish Thakor
- Touch and Proprioception
### Panel
- 


## Known Good Designs - Analog Blocks
[Link](https://github.com/USCPOSH/AMS_KGD)


## Analog Neuromorphic Technologies
- ![Pasted image 20210629130417.png](Pasted%20image%2020210629130417.png)
- ![Pasted image 20210629130443.png](Pasted%20image%2020210629130443.png)
	- MAC -> multiply-and-accumulate
- FPAA
	- ![Pasted image 20210629131121.png](Pasted%20image%2020210629131121.png)
### Floating Gate Circuits
- ![Pasted image 20210629131635.png](Pasted%20image%2020210629131635.png)
- Synaptics -> early FG synapses
- ![Pasted image 20210629131831.png](Pasted%20image%2020210629131831.png)
	- Doesn't scale well to lower tech. nodes
	- Injecting pFETs fix the problem
	- Can make ADCs, DACs, filters etc.
- ![Pasted image 20210629132333.png](Pasted%20image%2020210629132333.png)
- ![Pasted image 20210629132345.png](Pasted%20image%2020210629132345.png)
- ![Pasted image 20210629132609.png](Pasted%20image%2020210629132609.png)

## FPAA - Jennifer Hasler
- FG device
	- ![Pasted image 20210629171718.png](Pasted%20image%2020210629171718.png)
- A single FG pFET can approximate an ideal switch in FPAA routing crossbar
	- ![Pasted image 20210629172541.png](Pasted%20image%2020210629172541.png)
	- A single pFET device is a good switch over the entire operating range, because the FG voltage can exist above or below the power supply rail.
- PUF using FGs
	- ![Pasted image 20210629174520.png](Pasted%20image%2020210629174520.png)
- How to program millions of FGs
	- Open source tool
	- Scilab/XCOS
- 

## ANT Lecture 1
- Even if von-Neumann bottleneck isn't there (eg. GPUs), processors working together require data to be moved around -> energy constraint

## Biological Backpropagation
- Weight transport problem 
	- Neurons can't know weights of connections to all downstream neurons
	- Can we infer weights from spike rates?
		- Spike timing dependent weight inference (STDWI) (almost looks like STDP)


## ANT 3 - Kwabena Boahen
- Power law asymptote explanation
- ![Pasted image 20210702220659.png](Pasted%20image%2020210702220659.png)
- ![Pasted image 20210702220849.png](Pasted%20image%2020210702220849.png)

## Neuromodulation - Terrence Sejnowski
- Otto Loewi - adrenaline, acetocholine
- Entire population need not be modulated for effects to be seen


## Nengo
![Pasted image 20210705120005.png](Pasted%20image%2020210705120005.png)
![Pasted image 20210702013951.png](Pasted%20image%2020210702013951.png)

- Feynman Lectures on Computation

Reservoir Computing
- Random neurons and connections
- Linear readout

![Pasted image 20210708211256.png](Pasted%20image%2020210708211256.png)

## Braindrop
- How to get diverse weights
	- Use resistor mesh -> each neuron is going to get different combination of inputs
- Tap point -> location on R mesh that accepts input
- 2 or more tap points per dimension
- ![Pasted image 20210709184635.png](Pasted%20image%2020210709184635.png)
	- Middle -> actual preferred directions from mesh
	- Bottom -> desired preferred directions -> gain control on neurons
- ![Pasted image 20210709185101.png](Pasted%20image%2020210709185101.png)
	- Place synapse at input tap points instead of at neuron input
- ![Pasted image 20210709185310.png](Pasted%20image%2020210709185310.png)
	- Top -> Poisson
	- Middle -> IF neuron
- ![Pasted image 20210709185703.png](Pasted%20image%2020210709185703.png)
	- Opponent pairs
- ![Pasted image 20210709185836.png](Pasted%20image%2020210709185836.png)
- ![Pasted image 20210709185849.png](Pasted%20image%2020210709185849.png)
	- Mismatch is good but some neurons are useless
	- Hence programmable gains and biases are required
- ![Pasted image 20210709190213.png](Pasted%20image%2020210709190213.png)
- ![Pasted image 20210709190549.png](Pasted%20image%2020210709190549.png)
	- Digital integrating neuron
- ![Pasted image 20210709190638.png](Pasted%20image%2020210709190638.png)
- ![Pasted image 20210709190734.png](Pasted%20image%2020210709190734.png)
- [Braindrop](https://drive.google.com/file/d/1qhqBRRQEnLae7bFnrYNwjpL_HDJujfuF/view?usp=sharing)
- Post mismatch optimization

# SMI - Human motor control uses minimum cost trajectories
- ![Pasted image 20210712204846.png](Pasted%20image%2020210712204846.png)
- ![Pasted image 20210712204945.png](Pasted%20image%2020210712204945.png)

# Spike Coding
- ![Pasted image 20210712214342.png](Pasted%20image%2020210712214342.png)
- ![Pasted image 20210712214528.png](Pasted%20image%2020210712214528.png)


# OpenLane setup
-  docker install
-  git clone https://github.com/The-OpenROAD-Project/OpenLane.git
    cd openlane/
    make openlane
- sudo chmod 777 pdks
- copy sky130A folder to openlane/pdks folder
- cd openlane
- sudo make test
