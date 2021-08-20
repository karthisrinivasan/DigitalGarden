[[Research]] [[Neuromorphic]]

# The neuromorphic Mosaic: re-configurable in memory small-world graphs

[[Thomas Dalgaty]] [[Melika Payvand]] [[Giacomo Indiveri]]

## Mosaic Structure
- Small-worldness -> dense local connections, sparse long-range connections
- Efficient global coordination
- Found in biological systems often
- ![Pasted image 20210813121708.png](Pasted%20image%2020210813121708.png)
- New architecture to implement small world networks -> mosaic
- Split large crossbar into smaller ones
- Some for weights, some for routing

## Routing
- ![Pasted image 20210813122200.png](Pasted%20image%2020210813122200.png)
	- green -> memory, blue -> routing
- Routing block
	- NSWE routing structure in 2D
	- Has current comparator circuit to determine whether or not to transmit spike
	- Connected / not connected -> LCS / HCS of RRAM

## Implementation and Results
- Implemented in 130nm hybrid technology
- 10x better power consumption figures compared to AER processors
- Almost no drop in accuracy wrt software model
- ![Pasted image 20210813161828.png](Pasted%20image%2020210813161828.png)
- Robust to loss in weight accuracy

## Circuits
- Synapse circuit
	- ![Pasted image 20210813162052.png](Pasted%20image%2020210813162052.png)
- Neuron Circuit
	- ![Pasted image 20210813162109.png](Pasted%20image%2020210813162109.png)
	- Dotted inverters are current starved to introduce delay

