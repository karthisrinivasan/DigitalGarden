[[Research]] [[Neuroscience]] 
# [Why Neurons Have Thousands of Synapses, a Theory of Sequence Memory in Neocortex](https://www.frontiersin.org/articles/10.3389/fncir.2016.00023/full)
- [[Jeff Hawkins]]
- Majority of synapses are distal
- Single distal synapse insignificant
- Dendritic branches - independent pattern recognizers?
- Sequence: activation -> prediction -> activation ...
![[Pasted image 20210502190331.png]]
	- B - Pyramidal neuron 
	- C - Hierarchical temporal memory ([[Heirarchical Temporal Memory]]) model (software ims)

### Neurons Recognize Multiple Sparse Patterns
- 8-20 synapses in proximity activate => spike
	- => pattern detector
	- => all dendrites - multiple independent pattern detectors
	- 8-20 seems too small, but works if sparse patterns
- Non-linear dendrite segment - classifies by sub-sampling
- Redundancy: noise tolerance at cost of false positives, but still negligible increase
- Number of synapses per neuron >> no of synapses required to recognize pattern => 1 neuron many patterns
- But most patterns do not lead to action potentials, but instead facilitate prediction and learning
### Cortical Neuron Synaptic Inputs
- proximal dendrites - feedforward input
	- basic receptive field
- basal dendrites
	- see the activity preceding firing
	- depolarize but not enough to spike
	- priming - important state
	- fires earlier than usual and inhibits neighbors => creates sparsity
- apical synapse - top-down / backward excitation
	- depolarize but not enough
	- same as basal
- [[Heirarchical Temporal Memory]]
	- Models de0ndrites as coincidence detectors
	- 3 groups as above

### Networks learn Sequences
- What is the fundamental operation of the neocortex?
	- Learning and recalling sequences
- Requirements
	- Online learning
	- High order predictions
	- Many simultaneous predictions
	- Local learning rules (in space and time)
	- Robustness (noise, unanticipated inputs)
### Mini-Columns and Neurons: 2 Representations
- High order sequence memory requires 2 simultaneous reps
- 1 for feedforward, other for feedforward in particular temporal context
	- eg. abcd, xbcy 
	- 1 letter = sparse pattern
	- Two diff reps required for b,c depending on context
	- Need to know what to do after c based on what came before
![[Pasted image 20210502192230.png]]
- All have same receptive fields
	- Input converted to sparse mini columns
	- Unanticipated input - all active
	- Known input - sparse activity - unique
### Basal Synapses: The Key to Sequence Memory
- Basal synapses - learn transitions between input patterns
- Generate predictions
- If input keeps matching prediction, sequence continues
![[Pasted image 20210502193301.png]]
	- Black active, red depolarized predicted
	- a) A - unexpected input  - predicted b - if really b
	- b) ambiguous input - both predicted -> both active -> both predicted and so on
- Multiple simultaneous predictions are common
- All cells in mini column have same feedforward response but basal dendrites recover different patterns
- Overall activity level is low

### Apical Synapses: Top-Down Expectation
- Feedback connections provide expectation/bias
- New feedforward input - part of predicted sequence
	- Biases toward certain interpretations
![[Pasted image 20210502223715.png]]
	- Sparse if expected, highly active if not
	- Network previously learned bcd
- Lateral connections to basal dendrites - predict next input
- Top down to apical dendrites - predict multiple sequence elements simultaneously

### Synaptic Learning Rule
- Learning occurs by growing/removing synapses from 'potential synapse' pool.
- Hebbian learning at dendritic segment level, not neuronal level
- Potential Synapses:
![[Pasted image 20210502224305.png]]
	- Each dendrite segment of [[Heirarchical Temporal Memory]] neuron: maintain a potential synapse set
	- No. of potential synapses >> No. of actual synapses
	- Assigned permanence value - represents stage of growth 
		- 0: just created, going to grow
		- 1: fully formed
	- Value changed according to Hebb's rule
	- Synapse weight = signum(permanence value - threshold)
	- Enables online learning in noisy environment
	- Can start growing new synapses but act differently only after many exposures to same stimulus
	- Higher permanence value - harder to forget

### Results
- Simulation: No apical synapses
- Exhibits all 5 properties
![[Pasted image 20210502224822.png]]
	- Maximum possible performance: 50%
	- Only achievable using high order representations
	- Data stream is changed: model recovers after dip
	- Robustness to neuron damage
- Important parameters: spike threshold, synapses/pattern
	- Need sufficiently high values

### Discussion
- Basal - contextual pattern + next feedforward input
- Apical - feedback patterns + whole sequences
- Continuous learning
- Unique roles to synaptic integration zones
- Learning rules vary with integration zone
- Inhibitory effects not uniform across integration zones
- Biologically accurate
- Higher level + larger scale than SNN models
- Model full sets of dendrites and integration zones
- Does not deal with sequence timing

### Network Capacity and Generalization
- Sequence memory is really transition memory
- Only learns transition
- Capacity linear in cells/column and patterns/neuron
- Can represent non-Markovian spaces
- Can learn long range temporal dependencies
	- eg. same word in multiple sentences - different representations
- Capacity determined by no. of transitions to be learned (word1 -> word2)
- Generalizes well due to sparsity

### Testable Predictions
- Explains sparsity of activity during predictable sequences
- Explains higher activity during unanticipated inputs
- Predicts that current cell activity pattern contains information about past stimuli 
- One synapse per axon dendrite pair
	- Else presynaptic cell dominates the behavior of postsynaptic cell
	- Hence discourages multiple synapses
	- Axon to different dendrite on same neuron is plausible, though.
		- Localize within dendrite segment
		- Fast spiking inhibition should exist
- Mutual excitation within mini-column required
	- Existence/Mechanism unknown: [[Ideas+Thoughts]]
- All excitatory neurons are learning sequences in the neocortex
- Rapid learning in hippocampus - 'silent' synapse, later converted to active synapse. Pure hypothesis

### Methods
- N mini-columns per layer, M cells per column
- synapse == potential synapse here
- $a^t_{ij}$  :  activity of $i_{th}$ cell in $j_{th}$ column
- $\pi^t_{ij}$   :  predictive state
- Distal segment d of ij neuron : $D^d_{ij}$ 
- Segment contains synapses, each with permanence value
- Random initialization
- Random permanence initialization
- $W^t$  :  set of k columns that match feedforward input pattern - winning columns
- Active state calculated as: 
![[Pasted image 20210502232337.png]]
	- Activate if in winning column and predicted correctly previously
	- If not predicted previously, activate all cells in column
- Predictive state calculated as:
![[Pasted image 20210502232440.png]]
	- $\theta$  :  spike thresholds
- Updating segments and synapses:
	- $D^d_{ij}$  chosen such that:
![[Pasted image 20210502232605.png]]
	- Selects winning column with correct prediction and then selects the segments responsible for it
- If input was unpredicted, need to find new cell to assign that transition:
	- Select segment closest to being active
	- Reinforce the segment which satisfies:
![[Pasted image 20210502232755.png]]
	- Didn't activate **and** closest to active
- To perform reinforcement, new D is:
![[Pasted image 20210502232922.png]]
- Decay segments that didn't become active
	- Can happen in mistakenly reinforced by chance
![[Pasted image 20210502233002.png]]
- Two $\Delta D$s are added to $D$ every time step