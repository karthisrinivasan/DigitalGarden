[[Research]] [[Neuroscience]] 
# [A Theory of How Columns in the Neocortex Enable Learning the Structure of the World](https://www.frontiersin.org/articles/10.3389/fncir.2017.00081/full)

- [[Jeff Hawkins]]
- Neocortex - columns + layers
- Canonical circuit - repeated
- Previously:
	- try to minimize cortical wiring
	- anatomy based differentiation
- General Rules
	- Cells that receive direct input do not send axon outside local region; do not form long distance intra-layer connections
		- Eg. Layer 4
	- Cells driven by cells above form long range intralayer connections, also send out long axons.
		- Eg. Layer 2/3
- Network model based on above rules
- Single column - learn structure of complex objects (larger than receptive field)
	- Due to motion across time over object
	- Output layer activation stable during this motion
- Collaboration across columns
- Each column - signal representing location
- Input layer - allocentric location (relative to object) signal + sensory signal
- Features essentially
- Reach into black box and feel object with hand analogy
	- More fingers - faster
- Model should work for all sensory systems

### Model Description
- Extension of [[Sequence Memory in the Neocortex]]
- 2 layers of pyramidal neurons in columns
- Output layer of each column learns an object representation that is consistent with sensation
- Input layer: receives sensory input (feature) + location input (location of feature on object)
- Requirements:
	- Location of feature independent of orientation of object (accuracy in novel positions)
	- Nearby location have similar representations
	-  Noise tolerance

### Neuron Model
- [[Heirarchical Temporal Memory]]
	- Proximal - feedforward inputs
	- Distal, Apical - modulatory inputs

### Input Layer
- Mini-columns
- Feedforward - sensory input
- Modulatory - location input
- One cell chosen to learn current location
- Inference - lateral inhibition by successful cell
- Sparse representation

### Output Layer
- Active cells represent objects
- Object - representation in op layer + location representations in input layer
- Modulatory input from other output layer cells
	- Acts as positive bias
	- Will cause it to win and inhibit others
- If 2 columns have feedforward support for (A,B) and (B,C) - will converge to B

### Feedback Connections
- Output to input
- Optional
- Robustness to noise and location ambiguity

![[Pasted image 20210504103500.png]]

### Example
![[Pasted image 20210504104110.png]]
- Disambiguation of Objects with shared features
- $f_1$: ambiguous feature
	- Simultaneous invocation of union of representations
	- One for each object containing that feature
- Red - predictive state
	- All features consistent with objects active in output layer
	- i.e. all consistent sensations up to now
- $f_2$: new feature
	- Only cells consistent with both now active
- Subsequent sensations narrow down


### Learning
- Hebbian learning rule
- Learning isolated to dendritic segments
- [[Sequence Memory in the Neocortex#Synaptic Learning Rule]]
	- Growing/removing from potential synapse pool
	- Permanence values
- Input layer - feature/location combos
- Unknown feature - new cell chosen
	- Winning cell  - best modulatory input match
	- Form and strengthen modulatory connections with current location input
	- Apical dendrites form connections to active cells in output layer
- Output layer - representation of objects
	- New object - sparse set in output layer chosen to represent
	- Active while sensations happening
	- feedforward connection reinforced between these output cells and changing input cells 
	- Each output cell - pools over many feature/location representations in input layer
	- Dendrite segments in op cells 
		- Modulatory connection to active cells in own and nearby columns
- Reset output layer when new object introduced

### Simulation Results
- 500 objects sharing features
- 2,400 neurons total - arranged in mini columns and then in columns
- Unambiguous recognition happens when output layer representation overlaps with correct object significantly but not any other object

### Network Convergence
- Multiple columns working together - reduction in number of sensations required
	![[Pasted image 20210504110150.png]]
	
-  More objects in training set - more sensations required to decide
	![[Pasted image 20210504110348.png]]
	
-  Unique objects -> faster
	![[Pasted image 20210504110354.png]]
	
-  Performance almost as good as ideal observer with locations
	![[Pasted image 20210504110403.png]]
	
### Capacity
- How many objects can 1 column represent?
- More columns = more capacity?
- Capacity = max number of objects network can learn and recognize without confusion
- Effect of representational space, number of mini columns, number of neurons in output layer, number of columns
- $^nC_m$ objects can represented with $n$ mini columns, $m$ simultaneously active mini columns
- Similarly for $n$ output cells and $m$ active output cells
- Capacity limited by pooling capacity of output layer
- 1 column - 100s of objects before hitting this limit
- ![[Pasted image 20210504113013.png]]

### Noise Robustness
- Noise affects active bits without changing overall sparsity
- ![[Pasted image 20210504113853.png]]

### Mapping to Biology
- Evidence of this model in neocortex
- First layer :: Second Layer
	- Layer 4 :: Layer 2/3
	- Layer 6a :: Layer 5
#### L4::2/3
- L4 cells receive thalamic input from sensory core regions
- project to L2/3 and receive feedback from L2/3
- L2/3 - output cells
- Location signal before sensory input
- Location from L6a
#### L6a::5
- No exact mapping / unclear
- ![[Pasted image 20210504131834.png]]
- Thalamo-cortical (TC), Cortico-cortical (CC)
- Green - feedforward, Red - location signal
- a - L4::2/3 ; b -L6a::5

### Location Signal Origins
- Derivation unknown
- Might involve connections between 'what' and 'where' regions

### Physiological Evidence
- 4,6a : simple receptive fields
- 2/3,5: complex receptive fields
- Differentiation in case of known objects observed
- Border ownership
	- Cells with same receive fields eg. all edge detectors which fire for a single edge fire uniquely when multiple edges are present in input
	- "Edge ownership"
	- Grouping stable over time
	- Seen in output layer
	- Form of complex object modeling

### Relationship with Previous Models
- One of first to propose functional role of layers and columns
- Predictive coding: 
	- earlier work; this is better
- LAMINART model
	- consistent with this theory
	- mathematical basis provided by this

### Benefit of Cortical Columns
- [[The Mindful Brain]]: column definition
	- mini-columns bound by short range horizontal connections
- 1 column can learn full objects
- Multiple columns are better and faster
- Exact anatomical organization is an open issue
- Boundaries between columns  not strict
	- Key requirement: each column models different subset of sensory space and exposed to diff parts as sensors move

### Generation of Location Signal
- Neocortex patch needs to know where sensor will be after motion is completed
- Prediction of this should be separate for each part of sensor array
- Allocentric location signals must be made in place where somatic topology is granular:
	- eg. multiple semi-independent touch regions on each finger: brain region must be similar in structure
	- S1, S2 regions
- Don't know exact mechanism
- Current location + object orientation + movement -> new location prediction
- Grid cells perform a similar function
	- Encode location of animal's body relative to environment
	- Use path integration to predict new location
	- Combine current location, body movement, head direction
	- Dimensionless
- Grid cells older than neocortex
- Possible source of location signals
- No direct evidence, though
	- Evidence that cells in various cortex areas modulated by body movement + position
	- Motor areas also contain reference frames

### Inhibitory Neurons
- Mini column neurons mutually inhibit
- spiking cells prevent others
- Requires fast Winner-take-all inhibition
- Output layer inhibition need not be fast
- Broader inhibition necessary
- No explicit inhibitory neurons in model
- Encoded into activation rules

### Hierarchy
- Assumption: complete objects recognized at level where cells respond to input over entire sensory array
- Alternate here: all columns, even low level ones, capable of learning complete objects
- But hierarchy still required
- Depends on spatial extent and size though
	- Small size stimulus could be recognized with low level cols, larger size would require high level cols

### Vision, Audition etc.
- Apply model to vision
	- skin and retina move, seeing different parts at different times
- Vision also has discontinuities and non-uniformities
- Allocentric location signal determination would be different
- Similar argument for audition

### Testable Predictions
- Sensory regions contain cells stable over movements of sensor when seeing familiar obj
	- Sparse and specific to object
	- Low overlap with another set of such cells
- Layer 2/3 independently learn and model complete objects
- Output layer activity sparser after learning object
- Denser for ambiguous objects
- Output layers form stable representations
- Algorithmic explanation for border ownership

[[The Mindful Brain]]: Hypothesis of all neocortex cells doing same thing because they look same
controversial: not know what this function is
how could a single function be applicable to all sensory and cognitive processes?

