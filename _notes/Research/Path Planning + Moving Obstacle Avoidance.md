[[Research]] [[Neuromorphic]]

# Path Planning and Moving Obstacle Avoidance with Neuromorphic Computing

- Path planning on dynamic graphs using SNNs
- Algorithm to explore paths considering obstacles' movement

## Mapping SPSP to SNN
- Shortest Path Search Problem (SPSP)
- Node <-> Neuron
- Edge <-> Synapse
- Undirected edges <-> symmetric synapse pair
- Self-loop synapse for continuous firing
- Weights:
	- $\frac{1}{\delta} \quad i\neq j$
	- $1 \quad i=j$

## With Obstacles
- Some nodes in graph cannot be part of path
	- This set is dynamically changed
- New membrane potential
	- $V_old$ if passable
	- 0 otherwise
- Shortest time can be found by checking the smallest time T at which goal neuron fires
- ![[Pasted image 20210521102604.png]]
- For backward search of shortest path:
	- Stimulate goal neuron at t=0 and continue till start neuron fires (backward wave)
	- Sequence of firing neurons would give shortest path

