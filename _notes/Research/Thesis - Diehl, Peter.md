[[Research]] [[Neuromorphic]]

# Performant Spiking Systems

[[Peter Diehl]] [[Matthew Cook]] [[Giacomo Indiveri]]

## Converting DNNs to SDNs
- ReLU <-> IF neuron with no refractory period (firing rate approximation)
- Standard recipe	
	- Use ReLUs
	- Set bis to zero, train  with backprop
	- Map weights from ReLU to IF units
	- Use weight normalization  for better accuracy and convergence
- Causes of loss of performance
	- Not enough input to cross threshold
	- Input so high that >1 spike/timestep
	- Over/under activation of specific feature set

### Weight Normalization
- ![[Pasted image 20210630115924.png]]
- Better than all previous SNN methods on MNIST

## Sentiment Analysis on TrueNorth
- NLP Implementation on TrueNorth chip
- word2vec
- Question classification

