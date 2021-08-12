# A spiking network that learns to extract spike signatures from speech signals
- [[Amirhossein Tavanaei]]
- [[Neuromorphic]] [[Research]] 
- Discriminative non-recurrent SNN
- Mix of Hebbian and anti-Hebbian STDP
	- Forces selective behavior
### Previous work
- Template based 
	- Spike extraction followed by raster comparison using Longest Common Substring (LCS) Algorithm
- Rate Coded
	- STDP + BCM
	- BCM: Modified version of Hebbian rule to incorporate LTP+LTD with bounds on both
	- Also allows for forgetting/decay
	- 
- Dynamic Synapse Encoding
	- High complexity
	- Discretization helps
- Reservoir based
	- Near perfect with noise robustness
	- SNN / non-SNN
	- More expensive than single layer SNN

## Feature Extraction
- Time segments - speech frames
	- 50% overlap
	- Hamming windowed
	- Slower speech => larger windows
- Frequency Spectrum
	- More resolution needed in lower frequencies  - nature of speech
	- Band spacing - Fibonacci, M=5
	- Range: R=4000Hz
![Pasted image 20210508124945.png](Pasted%20image%2020210508124945.png)
- Feature: Average energy in frame

## Input Spike Generation
- Izhikevich regular spiking (RS) model
- Feature value controls injected current $I_{inj}$
- $I_{inj}=I_{tot}$ for input layer
- Higher total current => More frequent spikes
- Spike rate adaptation to constant input
- $C\frac{dV}{dt} = k(V−V_{rest})(V−V_{th})−U+I_{tot}$
- $\frac{dU}{dt} = a[b(V − V_{rest})−U]$
- Reset: if $V>V_{peak}: V=c , U=U+d, spike$
- U - Inhibitory factor for spike, keeps membrane potential near $V_{rest}$
 ![Pasted image 20210508130156.png](Pasted%20image%2020210508130156.png)

## Network Architecture
- N feature vectors, M components each
- Sequential information not lost, converted to geometric information
- NM input RS neurons
- 10 output layer RS neurons - 1 per digit
- Fully connected
- Teacher 
	- determine form of STDP to be used
	- Hebbian / anti-Hebbian

## Learning
- Two types
	- STDP for training input-output synapses
	- Inputs to output layer used to train SVM for classification
#### Neuron model
![Pasted image 20210508131002.png](Pasted%20image%2020210508131002.png)
- Input layer - only $I_{inj}$
- Output layer - only $G_k$
- Learning - modifying $G_k$
- Change of conductance on receiving one spike: $G(t)=K_{syn}te^{-t/\tau}$
- Synaptic conductance constant $K_{syn}$ adjusted during learning according to Hebbian rule: $\Delta K_{ji}=\Delta w_{ji}K_{ji}$ where:
$$
\Delta w_{ji}=
\begin{cases}
0.01Ae^{-|\Delta t|/\tau+}	&\Delta t\geq 0, A>0\\

0.01Be^{-|\Delta t|/\tau-}	&\Delta t< 0, B<0\\
\end{cases}
$$
- $\Delta t$ is the time difference between post-synaptic and pre-synaptic spike
- Hence, the total conductance of all the synapses coming in to a single output layer neuron is 
$G_{tot}=\sum_{k=1}^{NM}\sum_{j=1}^{N_{rec,k}}K_{syn}(t-t_{k,j})e^{-(t-t_{k,j})/\tau}$
- $t_{k,j}$ is the spike time of spike j for synapse k

#### Anti-Hebbian Rule
- Cases flipped in the $\Delta w$ update rule
- To force "unlearning" of one neuron's class by another neuron

## Results
### Training
- Random initialization of weights
- 100ms stimulation time per data point
- 200 synapses per output neuron => 2000 synapses
- When "1" is presented, 200 synapses of "1"-neuron undergo Hebbian, other 1800 undergo anti-Hebbian
- Weights renormalized after each data point
### Testing
- Prototype: Average input for that class
- Distance of sample from prototype: Victor-Purpura distance metric - dissimilarity of spike trains
### Classification
- Output from 10-neuron output layer used to train SVM
- 40 5ms frames (200ms total: 2x due to overlap)
- Features extracted (average energy) from this and given to SVM to do final classification
- 91% accuracy ideally, 70% with 10dB noise
- Can be used to detect sequence-of-numbers as temporal information is preserved
- Constrained by complexity; might not be suitable for large vocabularies