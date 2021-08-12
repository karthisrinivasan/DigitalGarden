[[Research]] [[Neuromorphic]] [[MITACS Project]]

# Overview of the SpiNNaker System Architecture

- [[Steve Furber]]

## Introduction
- Massively parallel multi-core computing system
- Packet communication
- Hierarchy
	- 1 node -> 2 silicon dice
		- SpiNNaker chip
		- DDR SDRAM
- 1,200 such boards
- 90kW max. power consumption

## Project Goals and Background
- More efficient parallel computing <-> better understanding of the brain
- Point neuron model
	- All inputs effectively at soma
	- Pure timing code
	- ![Pasted image 20210605193252.png](Pasted%20image%2020210605193252.png)
- Topological Virtualization
	- 3D -> 2D mapping can be arbitrary
- SpiNNaker core -> ARM9 processor
	- 1,000 neurons

## Architecture Overview
- ![Pasted image 20210605194945.png](Pasted%20image%2020210605194945.png)
	- SpiNNaker node
- Toroidal lattice
	- ![Pasted image 20210605195017.png](Pasted%20image%2020210605195017.png)
- SpiNNaker die
	- ![Pasted image 20210605195049.png](Pasted%20image%2020210605195049.png)
	- 18 subsystems (ARM cores)
	- 1 chosen to perform system management tasks -> Monitor Processor
- Routing
	- 32-bit payload AER packet

## System Components

### ARM968
- ![Pasted image 20210605201931.png](Pasted%20image%2020210605201931.png)
- core-local memories connected to processor

### Vectored Interrupt Controller (VIC)
- Enable/disable interrupts from various sources
- Wake processor from sleep

![Pasted image 20210605202135.png](Pasted%20image%2020210605202135.png)

## Memory Spaces
- Dedicated memory for each processor
- ![Pasted image 20210605202527.png](Pasted%20image%2020210605202527.png)
- ![Pasted image 20210605202549.png](Pasted%20image%2020210605202549.png)

## Routing Subsystem
- Asynchronous interconnect infrastructure
### Packet Taxonomy
- Types
	- Nearest neighbor
	- point-to-point
	- Multi-cast
	- Fixed route
- ~100ns latency

![Pasted image 20210606090338.png](Pasted%20image%2020210606090338.png)

#### NN Packets
- Launched from any core
- Delivered to monitor core
- Special type: peek-poke

#### Point-to-Point Packets
- Global synchronization must be accurate to within one time phase

#### Multi-case Packets
- Data transmission
- Direct core-to-core

#### Fixed-Route Packets
- Programmable fast track
	- Usually to nearest Ethernet-enabled node

### Initializing the Router
- Each node connected to 6 neighbors, internal port addresses of each link known
- Define routing tables
- ![Pasted image 20210606091250.png](Pasted%20image%2020210606091250.png)
	- Want to go to 'x', send through 'y'
- ![Pasted image 20210606091413.png](Pasted%20image%2020210606091413.png)

### Router Internals
- ![Pasted image 20210606091558.png](Pasted%20image%2020210606091558.png)
- Source key input to CAM
- Drives lookup RAM
- Packet duplication and routing

### Networks-on-Chip
- Delay-insensitive asynchronous logic
- Robust to timing issues
- No timing validation required
- Cost - extra information embedded in protocol
	- But not too bad due to absence of fast clocks, good data encoding
- 
#### System NoC
- Handle on and off-chip inter-processor communication
- Allow up to 16 processors to share 1Gbps SDRAM
- Provide independent access for Monitor Processor to resources

#### Communication NoC
- Handle on=chip processor-memory and processor-peripheral communication
- ![Pasted image 20210606092234.png](Pasted%20image%2020210606092234.png)
	- Merges various packet sources into one stream
- Transforms data into DI NRZ protocol to drive output ports

## Fault Tolerance
### Processors
- Node watchdog catches rogue software
- Periodic self-test interrupt handlers can be run
- Individual ARMs can locked out

### Interrupt Controller
- Entire node locked out in case of error
- Almost impossible to detect erroneous invocation

### Counters/Timers
- Periodical calibration
- Can be disabled

### DMA
- CRC error detection is built into hardware
- Node needs to be closed down

### Packet Communications
#### NN Peek-poke
- Used to access System NoC resources of neighboring chip
	- Investigate nonfunctional chip
	- Reassign Monitor Chip
	- Visibility for test/debug purposes
#### Low-level Error Control
- Rerouting packets in case of link blockage
- Transient congestion -> do nothing
- Recurring congestion -> establish new route for some traffic
- Out-of-order delivery possible
#### Communication Router
- Can map out failed multi-cast router entry
- P2P packets routed around obstruction
- MC packets rerouted as P2P payloads and resurrected
- Errant packets usually dropped to Monitor Processor
- Multi-cast router entry can be disabled if it fails
- Router becomes full -> global reallocation of resources -> difficult

### Interchip Communication
- Glitch may introduce packet errors
- Unlikely to cause deadlock
- Monitor Processors regularly test link

## Physical Assembly
- 1 node -> 1W
- 75W per board

## Software
- PyNN to SpiNNaker mapping

