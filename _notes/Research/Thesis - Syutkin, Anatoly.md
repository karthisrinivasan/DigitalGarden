[[Research]] [[Neuromorphic]] [[MITACS Project]]

# Hardware Implementation of Spiking Neural Networks
- Anatoly Syukin [[Glenn Cowan]]
- Scalable architecture for SNN IC

## SNN IC Architecture
- Voltage signal encoder, SNN IC, spike-train converter
- AER: need constant router delay, ideally none
- Event collisions -> arbiter
- Torus arrangement of cores
- External events to local neurons: content-addressable memory (CAM)

## Contributions
- Framework for study of designs and trade-offs
- Simulations
	- Weight quantization effect
	- Mismatch modeling (low impact on neuron, high impact on synapse)
	- Routers: primary cause of sim-to-hardware difference
	- Serialized spikes - slight divergence in concurrent events

## Background and Lit. Review
- [[DYNAP-SE]]
- [[SpiNNaker]]
- [[TrueNorth]]
- [[Loihi]]
- [[BrainScaleS]]

## Proposed Architecture
- ![Pasted image 20210603202530.png](Pasted%20image%2020210603202530.png)
- Platform for making design decisions
	- Type of neuron, synapse models
	- No. of neurons per core
	- Weight resolution
	- Max. no of synapses per neuron
- Enables study of mismatch, routing delays

### Core Operation
- N separate neurons 
- No. of synapses ~ $O(N^2)$
- One synapse/neuron
- Neurons <-> arbitration module <-> router
- Memory array for biasing currents
- Memory grid for local synapse weights
- External memory for inter-core synapses
- Address Event Representation
	- Spike event
	- Arbiter excited
	- Address stored in event buffer (queue)
	- Router retrieves weight based on event address
	- Current pulses injected into synapses, with appropriate amplitude
- One spike at a time into a synapse
- $O(N^2)$ issue not fully fixed due to memory requirement for weights
- Tiling of multiple cores -> easy
	- 4 Rx and 4 Tx ports per core

### Scaling
- M cores, N neurons per core
- No. of entries that each router can handle: (M-1)xN
- In normal grid, cores at corner have some ports under-utilized
- Torus arrangement solves this
- ![Pasted image 20210604092537.png](Pasted%20image%2020210604092537.png)

### Local Router Bridge
- Redistribution of local events without router
- FSM -> spike acknowledge signals, synapse triggers
- Disadvantage: inability to broadcast local events across cores
- Hence only used on cores that don't have off-core destinations
- Can be bypassed if needed
- ![Pasted image 20210604092935.png](Pasted%20image%2020210604092935.png)

### Memory Programming
- Total address bus length `IC_PROG_ADDR`
	- `ALEN_ICS + 2ALEN_NRNS + 3`
	-	`ALEN_ICS`: Address length for cores
	-	`ALEN_NRNS`: Address length for neurons
		-	2x for X,Y coordinates
- ![Pasted image 20210604093402.png](Pasted%20image%2020210604093402.png)
	-	XY: 2 MSBs
	-	Z: At index `2ALEN_NRNS`
- ![Pasted image 20210604093637.png](Pasted%20image%2020210604093637.png)

## Design of an SNN Core
- Memory modules for biasing currents, synaptic weights, routing tables

### RAM
#### Stack 
- Array of registers
- Simultaneous R/W
- ![Pasted image 20210604094108.png](Pasted%20image%2020210604094108.png)
- `MEM_RST` and `MEM_CS` -> 1
- Write enabled
- `MEM_ADDR_W` incremented and corresponding register written into
- `MEM_ADDR_R` enabled, output in `MEM_OUT`
- ![Pasted image 20210604094235.png](Pasted%20image%2020210604094235.png)

#### Grid
- Array of stacks
- `MEM_ADDR_Y` to determine stack
- `MEM_ADDR_X` for word inside specified stack
- Input, single bus: `MEM_IN` of `WIDTH`
- Output, multiple buses: `2^{ALEN_Y}WIDTH`
- All stacks have direct output bus
	- `MEM_ADDR_Y` can be ignored during read
- ![Pasted image 20210604095213.png](Pasted%20image%2020210604095213.png)
- ![Pasted image 20210604095540.png](Pasted%20image%2020210604095540.png)
- ![Pasted image 20210604095547.png](Pasted%20image%2020210604095547.png)

#### Content Addressable Memory
- Dictionary data structure
- Accept keyword and output associated value
- Routing table implemented with CAMs
- Match Cell
	- 1 register + small comb. circuit
	- ![Pasted image 20210604095835.png](Pasted%20image%2020210604095835.png)
	- Complete match between `MC_KEY` and output
	-	`MC_MATCH` high if key = initially programmed value
	-	![Pasted image 20210604100039.png](Pasted%20image%2020210604100039.png)

- Match Array
	- `DEC_ONE`: decodes address into one-hot
	- Output vector is concatenation of all match lines
	- If all keys unique, `CAM_MATCH` at most one-hot
	- Duplicates -> several logical ones -> possible corruption
	- ![Pasted image 20210604101428.png](Pasted%20image%2020210604101428.png)
	- ![Pasted image 20210604101440.png](Pasted%20image%2020210604101440.png)
	- ![Pasted image 20210604101449.png](Pasted%20image%2020210604101449.png)

- CAM Stack
	- Matching array + memory stack
	- Output of matching array -> one-hot to binary using `ENC_ONE`
	-	Used to access memory and value is retrieved
	-	![Pasted image 20210604101718.png](Pasted%20image%2020210604101718.png)
	-	![Pasted image 20210604101837.png](Pasted%20image%2020210604101837.png)
		-	Sequential programming of 4 pairs

- CAM Grid
	- Matching array + memory grid
	- Output buses concatenated -> `MEM_CSA` (chip select all) high -> all stacks accessed at once
	- ![Pasted image 20210604102027.png](Pasted%20image%2020210604102027.png)
	- Similar to CAM stack, with more values
	- One key -> multiple values
	- $2^{alen_x}-1$ keys, $2^{ALEN_Y}$ values per key
	- ![Pasted image 20210604103056.png](Pasted%20image%2020210604103056.png)
	- ![Pasted image 20210604103107.png](Pasted%20image%2020210604103107.png)

### Neurons and Synapses
#### Neuron
- First iteration
	- LIF with floating point weights
	- ![Pasted image 20210604152452.png](Pasted%20image%2020210604152452.png)
- Pos-edge of `CLOCK` triggers `PROCESS` statement that updates state variable, and compares with threshold
- Pre-synaptic current - floating point
- Bias current - binary coding
- After spike, neuron operation halted until `ACK` signal is received

#### Synapse
- Output is a single floating-point number
- ![Pasted image 20210604154600.png](Pasted%20image%2020210604154600.png)
- Current inputs always connected to memory modules' outputs
- Additional control signals to restrict input to impulses: `PULSE_MEM`, `PULSE_CAM`
- ![Pasted image 20210604154736.png](Pasted%20image%2020210604154736.png)

#### SN Column
- ![Pasted image 20210604154811.png](Pasted%20image%2020210604154811.png)
- All input vectors of size NUMxRES
	- NUM: No. of SN pairs
	- RES: Resolution of current input
- Output - single bus `SN_OUT`, size NUM
- `SN_ACK` for acknowledge bits

### Arbitration
- Serialize events, encode address and deliver to local router
- Release signals to neurons that spiked, allowing reset
- Fundamental tree structure
- Root has short circuit to get generate acknowledge signals
- ![Pasted image 20210604155301.png](Pasted%20image%2020210604155301.png)

#### Arbitration Latch
- ![Pasted image 20210604155347.png](Pasted%20image%2020210604155347.png)
- If both neurons generate event in close succession, must wait for first to acknowledge before transmitting second
- Need high symmetry
- Alternating priority to both outputs -> balance in fast-firing cases
- ![Pasted image 20210604155649.png](Pasted%20image%2020210604155649.png)
- ![Pasted image 20210604155657.png](Pasted%20image%2020210604155657.png)

#### Arbitration Node
- Combines both latch outputs into one
- Also transmits acknowledge signals
- `AN_REL1, AN_REL2`: Acknowledge latched neurons
- Also used to indicate address: `AN_ADDR`: 0 for 1st neuron, 1 for 2nd
- ![Pasted image 20210604160027.png](Pasted%20image%2020210604160027.png)
- Delay+AND -> Glitch at output when outputs switch from $s_1$ to $s_2$ directly
	- If both are firing fast, latch never goes into idle
	- Larger arbitration tree stuck on these two neurons
	- Rest of the network ignored
	- => introduce dead time $t_D$ to glitch the output to 0
- ![Pasted image 20210604160317.png](Pasted%20image%2020210604160317.png)

#### Arbitration Column
- ![Pasted image 20210604160358.png](Pasted%20image%2020210604160358.png)
- Combination of nodes
- Outputs `AN_ADDR` of each node from same column - connected together
- 1 column -> 1 bit of the address event

#### Arbitration Tree
- Cascaded arbitration columns
- Leaf (leftmost) column -> LSB, Final column -> MSB
- ![Pasted image 20210604160632.png](Pasted%20image%2020210604160632.png)
- No. of nodes = 0.5x no. of nodes in previous column
- ![Pasted image 20210604160804.png](Pasted%20image%2020210604160804.png)
	- Testing with one-hot inputs
	- Delayed acknowledge signal supplied at root
	- Release vector `AT_REL` that matches input
	- Address of high bit encoded
	- Multiple 1s decoded sequentially
	- Dead-time glitch at 18ns, 26ns

#### Arbiter
- Tree is asynchronous for analog neurons with arbitrary spiking times
- But need DFFs to interface with local router IC
- ![Pasted image 20210604161120.png](Pasted%20image%2020210604161120.png)
- When neuron spikes, arbiter input has a one-hot input
- Address encoded by tree
- `ARB_EVENT`, `ARB_UNH` given to local router
- After router registers events, release signal given to neuron
- Ready for next event
- ![Pasted image 20210604161457.png](Pasted%20image%2020210604161457.png)

### Routing
- Interconnecting multiple cores
- ![Pasted image 20210604161931.png](Pasted%20image%2020210604161931.png)
- Minimum possible delay, compared to time constants
- Rx: accept external events, sends to local neurons/other Tx
- Tx: Send spikes encoded as source addresses from local router/other 3 Rx

#### Router Communication
- Signals (Rx-polarity/Tx-polarity)
	- `EVENT`: bus transmitting event address (i/o)
	- `UNH`: event is unhandled (i/o)
	- `ACK`: event is acknowledged (o/i)
- ![Pasted image 20210604162528.png](Pasted%20image%2020210604162528.png)
- Operation
	- Event transmitted on `EVENT` and `UNH` raised
	- Rx port raises `ACK` to indicate storage in buffer
	- `UNH` asynchronously reset

#### Event Buffer
- Circular buffer
- Pointers: 
	- `HEAD`: New event written in
	- `TAIL`: Event being delivered read out
- ![Pasted image 20210604162752.png](Pasted%20image%2020210604162752.png)
- INCR - counters, width = no. of address bits in stack
- ![Pasted image 20210604162844.png](Pasted%20image%2020210604162844.png)
- New event appears in `EB_IN`
	- `EB_TRIG` triggered to save
	- `HEAD` incremented
	- `EB_FLAG_UNH` raised to indicate undelivered event
- ![Pasted image 20210604163057.png](Pasted%20image%2020210604163057.png)
	- `TAIL` incremented as events delivered
	- Once caught up with `HEAD`, `EB_FLAG_UNH` reset

#### Transmitting Router
- No routing tables
- 4 inputs, 1 output
- Connected to local and 3 opp. Rx routers
- ![Pasted image 20210604192644.png](Pasted%20image%2020210604192644.png)
- `incr`: 4 states to iterate through input ports and handle
- FSM: Save incoming events onto buffer
- ![Pasted image 20210604193018.png](Pasted%20image%2020210604193018.png)
	- `EB_FLAG_FULL`,`EB_FLAG_UNH` on transitions
	- Control 3 signals to increment, latch-in and increment `HEAD`
	- ![Pasted image 20210604193124.png](Pasted%20image%2020210604193124.png)
- Multiple events at all ports:
- ![Pasted image 20210604193220.png](Pasted%20image%2020210604193220.png)
	- Events without `UNH` flags are ignored

#### Receiving Router
- Same as Tx, with routing table implemented with CAM
- ![Pasted image 20210604193420.png](Pasted%20image%2020210604193420.png)
- Output of event buffer -> key for CAM stack
- `BCAST` device:
	- ![Pasted image 20210604193709.png](Pasted%20image%2020210604193709.png)
- Event being delivered
	- Retrieve directions from routing table
	- Retrieve value and latch onto DFFs, apply to broadcast device
- `FSM_HEAD`: ensure event buffer is not full
- `FSM_TAIL`: monitors unhandled events in buffer
- ![Pasted image 20210604194119.png](Pasted%20image%2020210604194119.png)
- ![Pasted image 20210604194136.png](Pasted%20image%2020210604194136.png)
- ![Pasted image 20210604194228.png](Pasted%20image%2020210604194228.png)

#### Local Router
- Receives from all 4 Rx router, transmits to all Tx routers.
- Combination of one Tx and 1 Rx router. 
- 2 event buffers
	- one for delivering to local neurons, 
	- one for broadcasting local events outwards
- ![Pasted image 20210604194405.png](Pasted%20image%2020210604194405.png)
	- `R_CAM_EVENT` - delivers external events
	- `R_MEM_EVENT` -  delivers local events and retrieves synaptic values from MEM grid
- ![Pasted image 20210604194449.png](Pasted%20image%2020210604194449.png)
	- Routing table programmed
	- Local events sent to input
	- Yellow - events being delivered to local SNs

#### Combined Router
- ![Pasted image 20210604194554.png](Pasted%20image%2020210604194554.png)
- Register added to first select line of address decoder
	- Store address of IC
	- IC address appended to address of firing neuron to indicate full origin

#### Local Router Bridge
- Jumper Module:
- ![[Pasted image 20210604194736.png]]
- `J_EN` - connected to select pin of all mux's, demux's
- When disabled, arbiter output -> router input
	- Router directly accesses memory grid with `MEM_ADDR`
	- Direct connection to `SN_TRIG` to inject current values
	- Short delay between access and activation
- `SPIKE_SINK` - receives interrupt on `UNH` pin and acknowledges event with 1 clock delay
- Jumper enabled:
	- `EVENT` bus of arbiter used to access synapses in local memory grid
	- `SPIKE_SINK` triggers synapses to release neurons

## Interface

### Input Encoding
- Input layer converts network inputs into spike trains
- ![Pasted image 20210604195244.png](Pasted%20image%2020210604195244.png)
- Spike generator:
	- ![Pasted image 20210604195311.png](Pasted%20image%2020210604195311.png)
	- Limited resolution
	- Constant biases
	- Slower clock to reduce power consumption
	- Time constants adjusted accordingly

### Output Decoding
- Image classification task
	- Accumulator
	- Allow settling to constant rate
	- Pick one that has emitted largest number of spikes
- First-to-spike decoding
	- Terminated when spike happens
	- Difficult to mitigate transient effects
- ![Pasted image 20210604195632.png](Pasted%20image%2020210604195632.png)
	- `EVENT` bus applied to demux
- Time-dependent solutions
	- LPF on spike trains

## Benchmarks
### MNIST
- M cores, N neurons
- $m=\lceil{log_2M}\rceil$
- $n=\lceil{log_2N}\rceil$
- ![Pasted image 20210604200411.png](Pasted%20image%2020210604200411.png)
- 30 hidden layer neurons
- ![Pasted image 20210604200432.png](Pasted%20image%2020210604200432.png)
	- Drop in 4 bits - many weights rounded to zero

#### Impact of Parametric Variation
- ![Pasted image 20210604200807.png](Pasted%20image%2020210604200807.png)

#### Modeling DAC Variation
- Current DAC to convert weight word into current value
- ![Pasted image 20210604200859.png](Pasted%20image%2020210604200859.png)
- $I_{OUT}=I_{REF}\sum_0^{N-1}(2^k+\nu_k)b_k$
	- $\nu_k$: current factor mismatch in FETs
	- ![Pasted image 20210604201042.png](Pasted%20image%2020210604201042.png)
	- Larger FET -> more current -> higher absolute mismatch
- Accuracy variation with DAC mismatch
	- ![Pasted image 20210604201341.png](Pasted%20image%2020210604201341.png)

### Cart Pole Balancing
- ![Pasted image 20210604201650.png](Pasted%20image%2020210604201650.png)
- Need to maintain rod upright
- Only horizontal force on cart can be controlled
- ![Pasted image 20210604201731.png](Pasted%20image%2020210604201731.png)
	- 2 output neurons, LPF'd, compared and converted to actuator signal
- ![Pasted image 20210604203511.png](Pasted%20image%2020210604203511.png)
- ![Pasted image 20210604203521.png](Pasted%20image%2020210604203521.png)
	- 4KHz clock for neurons
	- 1KHz clock for spike generator
- Use of local router worsens performance due to delay
- ![Pasted image 20210604203635.png](Pasted%20image%2020210604203635.png)

## Future Work
### Fabrication
- Allow for neuron to resume operation without waiting for arbiter
- Modify local router bypass such that some events can go through bridge, others through Tx routers
- Separate clocks for SNs and routers
- Better models of neurons and synapses
- Calibration circuits for robustness against process variations
- Physical Layout

### Investigations
- STDP and its effects
- Learning algorithms
- Izhikevich model
- Alternate routing schemes and topologies
	- Multiple spikes/packet
- Dynamic element matching in DAC