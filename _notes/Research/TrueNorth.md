[[Research]] [[Neuromorphic]] [[MITACS Project]]

# TrueNorth: Design and Tool Flow of a 65mW 1 Million Neuron Programmable Neurosynaptic Chip

[[Filipp Akopyan]] [[Rajit Manohar]]

![Pasted image 20210606122441.png](Pasted%20image%2020210606122441.png)
Neocortical column -> Neurosynaptic core
Tiling of cores -> TrueNorth chip
Approximation of cortical structure

Design Principles
-	Minimize active power
-	Minimize static power
-	Maximize parallelism
-	Real-time operation
-	Scalability
-	Defect tolerance
-	Hardware-software one-to-one equivalence

5.4 billion transistors

## The TrueNorth Architecture
- ![Pasted image 20210606124840.png](Pasted%20image%2020210606124840.png)
- Synchronized spike distribution (1ms tick)
- Intra-chip and inter-chip spike communication
- ![Pasted image 20210606125606.png](Pasted%20image%2020210606125606.png)

## Mixed Synchronous-Asynchronous Design
- Asynchronous for communication and control
- Synchronous for computation
- No high-speed global clock
- QDI design
	- Synchronize by communicating tokens over delay-insensitive channels
	- Implemented using 4-phase handshake protocol
- Single bit protocol:
	- ![Pasted image 20210607090049.png](Pasted%20image%2020210607090049.png)
- QDI asynchronous pipelines
	- Pre-charge half-buffers (PCHB)
	- Pre-charge full-buffers (PCFB)
	- Weak-condition half-buffers (WCHB)

## Chip Design
### High Level Description
- ![Pasted image 20210607090459.png](Pasted%20image%2020210607090459.png)
- 64x64 neurosynaptic cores
- 1 core: Schedulaer, Roken controller, core SRAM, neuron, router

#### Neuron Block
- Augmented I&F
- Synchronous but event-driven
- ![Pasted image 20210607091902.png](Pasted%20image%2020210607091902.png)
- Core SRAM stores weights, leak, threshold, configuration parameters and membrane potential
	- Read and written every cycle

#### Router
- ![Pasted image 20210607092153.png](Pasted%20image%2020210607092153.png)
- 6 processes: to/from local, forward N/S/E/W
- XY routing
	- Repeater cores for distances greater than 4 cores in either direction
	- EW prioritized over NS -> prevent deadlock
- Back-pressure
	- Router stalls previous link in chain to reduce congestion (can go all the way back to generating core)
	- Communication time between neurons thus depends on traffic
- Built-in buffers and hierarchical communication reduce traffic

#### Scheduler
- Receives packets from router
- Delivers to neuron at right tick
- Packet:
	- ![Pasted image 20210607094040.png](Pasted%20image%2020210607094040.png)
	- delivery tick least significant 4 bits => need to deliver within 15 ticks of spike generation
- ![Pasted image 20210607094243.png](Pasted%20image%2020210607094243.png)

#### SRAMs
- One for spike queue, one for SN parameters
- ![Pasted image 20210608100050.png](Pasted%20image%2020210608100050.png)
- Core SRAM
	- ![Pasted image 20210608100144.png](Pasted%20image%2020210608100144.png)
	- Redundant circuits since most defects happen here

#### Token Controller
- ![Pasted image 20210608100305.png](Pasted%20image%2020210608100305.png)
- Dendritic approach
	- Request activity of neuron upon tick
	- Repeat for 256 neurons: (j)
		- Read neuron data
		- Repeat for 256 neurons: (i)
			- Send compute instructions if spike and weight are both 1
		- Apply leak
		- Check threshold, reset if needed
		- Send spike to router
		- Write potential to SRAM
	- Report errors
- Contrast to Axonal Approach, which handles every input spike as an event that triggers multiple SRAM ops

#### Periphery - Merge-Split Blocks and Serializer-Deserializer Circuits
- 64 bidirectional ports every edge
- ![Pasted image 20210608101111.png](Pasted%20image%2020210608101111.png)
- M-S block
	- Mux and demux packets onto a single port
	- Merge-Serializer path -> sending spikes from the core array to the I/O
	- Deserializer-Split path -> receiving spikes from I/O and sending them to cores
- ![Pasted image 20210608101538.png](Pasted%20image%2020210608101538.png)

#### Periphery - Scan Chains and I/O
- 8 10MHz scan chains per core for programming
- 64 cores in a row share scan interface
- Same row cores can be programmed simultaneously

## Chip Design Methodology
- ![Pasted image 20210607095011.png](Pasted%20image%2020210607095011.png)
- Signal integrity issue such a a glitch may cause deadlock
	- minimized the wire cross talk noise
	- reduced gate-level charge sharing
	- maximized slew rates 
	- confirmed full-swing transitions on all asynchronous gates

### Timing Design
- Mutually exclusive timing of sync/async:
- ![Pasted image 20210607095805.png](Pasted%20image%2020210607095805.png)
- Token controller generates synchronous clock and data:
- ![Pasted image 20210607095841.png](Pasted%20image%2020210607095841.png)

## Measured Data
- ![Pasted image 20210607100047.png](Pasted%20image%2020210607100047.png)
- 2-3 orders of magnitude speedup
- 5 orders of magnitude lower power

## Applications
- Wire length minimization
	- Logically connected cores -> physically closer on chip
	- Better efficiency
- ![Pasted image 20210607101115.png](Pasted%20image%2020210607101115.png)
- ![Pasted image 20210607101123.png](Pasted%20image%2020210607101123.png)
- Power Results:
- ![Pasted image 20210607101002.png](Pasted%20image%2020210607101002.png)

## Future Large-Scale System
- 2096 chips per stack -> 4 billion neurons, 300W
- 96 racks -> ~ human brain, 29kW
- Real-time simulation
