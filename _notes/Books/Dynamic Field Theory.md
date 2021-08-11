[[Books]] [[Neuroscience]] 

# Dynamic Thinking: A Primer on Dynamic Field Theory

# Foundations of Dynamic Field Theory

### Introduction
- Provides neural process accounts for a large swath of behaviors and cognitive abilities

### History of Ideas
- Roots in motor/muscle control theory
- Stability is N&S for coordination patterns
- Can cognition arise directly from action-perception in closed loop
- Representational states
- Biological models do give rise to DFT dynamics
- DFT valid all the way from motor behavior to higher cognition
- Integration: follow common principles
---
 ## Chapter 1
### Foundations
- [[Braitenberg Vehicle]] - neural account of behavior
	- Sensors, effectors, nervous systems, bodies
	- ![[Pasted image 20210513090719.png]]
	- Taxis vehicle - orients towards stimulus
	- ![[Pasted image 20210513090909.png]]
	- Structured environment - meaningful behavior
	- fifth component of the vehicle
	- vehicle + environment - dynamical system
- C1 - closed loops to create internal attractor states that are active even after input is removed
- C2 - origin of neural activation variables
- C3 - neural foundations of dynamic fields - real neurons
- C4 - behavioral dynamics + DFT = cognition

### Neural Dynamics
- Neural processes from which behavior emerges evolve continuously in time; linked to each other and sensory info
- stability essential
- dynamic instability
#### Activation
- activity of pops - related to behavioral patterns
- [[Mean Field Approximation]] - population activation vs. its rate of change - sigmoidal relation
- Discrete spiking events not accounted for in mean-field
- Continuous time approximation - spikes frequent enough
- Relation:
	- state of world influences activation level
	- activation level influences world through motor actions

#### Neural Dynamics
- $\tau\dot{u}=f(u)$
	- $u$ - activation variable
	- stability requirement
- Noise: $\tau\dot{u}=f(u)+q\zeta(t)$ 
	- $\zeta(t)$: AWGN 

>Euler's Numerical Method
>$u(t_i)=u(t_{i-1})+\Delta tf(u(t_{i-1}))$
>With noise:
>$u(t_i)=u(t_{i-1})+\Delta tf(u(t_{i-1})) + \sqrt{\Delta t}q\zeta(t_{i-1})$

- Noise addition to constant activation
	- $\tau\dot{u}=\zeta(t)$
	- ![[Pasted image 20210513105024.png]]
	- Random walk; Brownian motion
- With stabilizing force:
	- $\tau\dot{u}=-u+h+\zeta(t)$
	- ![[Pasted image 20210513105225.png]]
- Convergence to fixed point - relaxation

#### Self-Excitation and Detection Instability
- Interaction - recurrence
- $\tau\dot{u}=-u+h+s(t)+cg(u)$
	- $s(t)$ - input
	- $g(u)$ - sigmoid threshold
	- ![[Pasted image 20210513110839.png]]
	- ![[Pasted image 20210513110910.png]]
	- Bifurcation - collision/splitting of fixed points
- Detection instability  
	- decision that significant input has been detected
	- stabilized - held even if input drops
	- necessary in real systems
- If input drops low enough - back to monostable off regime
	- reverse detection instability
- Decision hysteresis
	- ![[Pasted image 20210513111626.png]]
	- inertia of response
	- detection of apparent motion - visual motion seen between location where there is luminance change
		- BRLC - background relative luminance contrast
		- motion detected at higher values
- Attractors are not stationary
	- Arise depending on input

#### Sustained Activation and Working Memory
- Stimulation does not uniquely determine inner state - hysteresis
- Working memory - bistable coexistence of off and on states
- Input triggers activation into on state, where it can remain indefinitely
- ![[Pasted image 20210513112523.png]]

#### Inhibitory Interaction and Selection
- Two activation variables
- $\tau\dot{u_1}=-u_1+h+s_1(t)-c_{12}g(u_2)+\zeta_1(t)$
- $\tau\dot{u_2}=-u_2+h+s_2(t)-c_{21}g(u_1)+\zeta_2(t)$
- Same resting level but different input, different noise sources
- ![[Pasted image 20210513112851.png]]
- Mutual inhibitory coupling
- Assume $u_2>0$ before $u_1$ left its resting level
- u1 gets pulled down
- u2 wins competition
- ![[Pasted image 20210513113215.png]]
	- Top: the gray line is the dynamics of u1 when u2 is sufficiently below zero so that the sigmoid yields zero.
	- Bottom: The solid black line is the dynamics of u2 when u1 is below zero.
- Activating one suppresses the other
- Attractor of second pushed way below zero
- Maintaining the selection decision
- Caveat: if input to suppressed variable is very high, it oculd overcome
- ![[Pasted image 20210513113522.png]]
	- Left: The dynamics of one of two competing activation variables is plotted in three cases: without external input (solid), and with external input but without (dotted) versus with (dashed) inhibition from the other activation variable.
	- Right: Activation trajectories for both activation variables are shown (one in solid black, the other in solid gray).
	- Same input but random fluctuations tip the balance
---
 
 ## Chapter 2
 - What exactly do activation variables 'stand for'?
 - Is truly categorical perception ever valid?
 - Continuous states of the world are primary

### Spaces
- Continuous variation of objects in vision
- Dimensions to describe real-world percepts
- ![[Pasted image 20210514180024.png]]

### Activation Fields
- Continuum of activation variables, labeled by continuous position
- Width, peak of activation field denotes preferred stimulus
- Peak of activation signify:
	- Fact that instance has been created that can affect other downstream networks (go signals)
	- Location of peak - metric information along the dimensions - estimate of perceptual state
- One stimulus followed by two:
- ![[Pasted image 20210514181439.png]]
- Depending on angular separation, network perceives three different things:
	- Averaging (fusion)
	- Splitting (transparency)
	- Selection

### Field Dynamics
- Activation field: $u(x,t)$
- Governing equation similar to single activation variable:
	- $\tau\dot{u}(x,t)=-u(x,t)+h+s(x,t)+ \int k(x-x')g(u(x',t))dx'$
	-  Integral is continuous version of sum over all field sites
	-  Each location $x'$ 's contribution weighted by $g$
	-  Strength of supra-threshold contributions - function $k(x-x')$ of distance between the sites
	-  $k(x-x')>0$ for close distances, $k(x-x')<0$ for larger distances
	-  Homogeneous - shifted versions of solutions also solutions
	-  Localized inputs $s(x,t)$ break homogeneity
	-  $k$ - analogous to synaptic weights
-  Boundary condition on convolution: Value at borders are same (periodic)
	-  Natural for circular fields like heading 
	-  Also works for things like visual field since activation diminishes at the edges

- Activation peaks - attractors
	- Local excitatory interaction stabilizes peaks
	- Inhibitory interaction over longer distances counter balances
	- ![[Pasted image 20210514183202.png]]

- Relation between activation fields and discrete activation variables
- ![[Pasted image 20210514183449.png]]
	- Global inhibition :: Mutual inhibition
	- Local Excitation :: Self excitation
- Local populations are the substrate for representation (not individual neurons)

### Attractors and Instabilities
- Sub-threshold and self-stabilized activation patterns
- Meaning of instabilities

#### Detection
- Simplest stable state - activation<0, only weak inputs
	- Interaction disengaged; field dynamics at each point independent
	- Stationary solution: sub-threshold attractor state
		- $u_0(x,t)=h+s(x,t)$
		- Disappears in presence of sufficiently strong input
		- ![[Pasted image 20210514190201.png]]
- Interaction engaged when activation approaches zero from below anywhere
- Gaussian input:
- ![[Pasted image 20210514191858.png]]
- New attractor - hill
- Reinforced by positive feedback
- Range of inputs exists where sub-threshold hill and peak are both stable : bistable state
	- But only one can be realized at a time
	- Which one depends on history of activation
- When input falls below a critical level, mechanism that keeps peak stable begins to fail
	- Reverse detection instability
- 'Detection Instability' described above - stable detection decisions even with fluctuating sensory input
- Emergence of discrete-time events (detection decision) from continuous time input
	- Peak remains coupled to continuously varying input afterwards, however
- Position of peak - estimate of location of maximum of input
	- peak tracks as input moves - lags behind though
	- may lose tracking if input fast enough - decay and formation of new peak when it detects again

#### Working Memory
- Reverse detection instability doesn't always occur
	- Large (less negative) resting level => lot of self-excitation
	- Sustained peak in absence of input
- Significance: memory of past locations of inputs
	- Accepted theory of working memory
- Sustained peaks <=> self-stabilized peaks
- ![[Pasted image 20210515100819.png]]
	- Left - monostable state in absence of input
	- Right - bistable in absence of input (larger h)
	- Self-stabilized peak actually continuum of attractors as location can be shifted along dimension

#### Selection
- In presence of multiple peaks in input, first peak to arise (depends on input and weight) stabilizes and suppresses others
- Input patterns that match pattern of synaptic connectivity provide strongest excitation
	- Lumped into $s(x,t)$
- First peak suppresses others even if input to those locations is stronger/equal later
- ![[Pasted image 20210515101800.png]]
	- Form of robust estimation
- Limitations:	
	- When input is sufficiently different, decision may be reversed
	- Selection instability
- Limit on number of simultaneous peaks - Inhibitory strength
	- Each peak inhibits rest of the region
	- Hence total number possible is limited
- Unlimited instabilities
	- Transition from multiple-peaks-stable to single-peak-stable
	- Transitions from n-stable to m-stable
- Two peaks in bistable move close to each other - transition to monostable
- Preshaping by inhomogeneous input + homogeneous brief boost => self-sustained peak
	- Can impact downstream dynamics by amplifying noise
	- Can alleviate demands on sensory input - they need to only deliver small amounts of input
		- Bootstrapping fields from sensory-motor domain
- 	![[Pasted image 20210515103035.png]]

#### Memory Trace
- Sustained peaks susceptible to capacity limits and interference
- Interference when new sensory information competes with existing peaks
- Learning - longer time scale than peak formation etc.
- Instance of self-excited peak formation - leaves memory trace that enables re-emergence of same peak
- ![[Pasted image 20210515103724.png]]
- Memory trace - second layer of dynamics on a slower time scale
	- Remembers past locations of peaks
	- Decays at locations where there are no peaks
	- Stays constant in absence of new peaks
	- Provides weak excitatory input back to activation fields thereby facilitating remembrance 
- $\tau_{mem}\dot{u}_{mem}(x,t)=-u_{mem}(x,t)=g(u(x,t))$
- $\tau_{mem}>>\tau$
- Coupling of memory trace and field dynamics:
- $\tau\dot{u}(x,t)=-u(x,t)+h+s(x,t)+ c_{mem}u_{mem}(x,t)+ \int k(x-x')g(u(x',t))dx'$
	- Strength : $c_{mem}$
- Memory trace does not evolve when no location has peaks
- Memory trace represents probability of events
- Example: 2-choice task where frequency of each task varies according to conditions
	- Response times vary with probability of each choice
	- Shorter for more frequent task
	- Memory trace converges to levels that reflect frequency of each choice - lead to pre-activation of field
	- Exact law - Response time ~ log(choice probability)
		- Arises from exponential time course of activation as it relaxes to the attractor
	- Prior probability representation based on history
	- ![[Pasted image 20210515104914.png]]
	- Trace becomes mechanism for category formation
	- Peak not at input location but actually at pre-shaped location
	- Will not vary with small changes in input location
	- Effectively a classifier now, parametrized by memory trace
	- Unsupervised learning

#### Illustration: DFT Model of Perseverative Reaching
- A-not-B task
- Trial on infants: 
	- Two wells A and B
	- Toy placed into A (in sight of infant) first few times, infants allowed to search, look in A first
	- Next time hidden in B, allowed to search, some look in A still
	- Stop making mistake around 1 year of age
- ![[Pasted image 20210515105858.png]]
	- Green - motor choice
	- Pink - Placing of object
	- Violet - Two discrete location
	- Grey - previous repetitions of task
	- Blue - Forcing choice by need for toy
- Large memory trace explains why mistake is made
- A trial:
- ![[Pasted image 20210515110235.png]]
- B trial:
- ![[Pasted image 20210515110314.png]]
	- Memory trace input lasts longer than stimulus input
	- B-peak decays at end of delay => A peak forms again
	- A-not-B error

- Older infants - higher resting levels of motor planning field (h)
	- Stronger interaction 
	- Push through memory instability
	- Sustained peaks in absence of input possible
- ![[Pasted image 20210515110707.png]]
	- B peak sustained - working memory regime
- Consequence:
	- Spontaneous errors in original A runs affect A-not-B error

- Sandbox task
	- On infants who would never make A-not-B mistake on original task
	- Toy buried in A/B locations in sandbox, allowed to dig
	- After many A-runs, dig in location near A even on B-run
	- Effect seen on children as old as 6 years
- No discrete locations like in previous task => no task input
- First B trial:
	- A and B location sufficiently close; peak at B affected by memory trace at A: 
	- ![[Pasted image 20210515111505.png]]
	- Cause of error here different from original task
	- Drift rather than forgetting as there is no input to keep peak centered at B
	- Memory trace wider due to drifting peak
	- A and B far apart; no metric bias:
	- ![[Pasted image 20210515111951.png]]
---

 ## Chapter 3: Embedding DFT in Neurophysiology
 - DFT not merely an analogy
 - Distribution of Population Activation (DPA)
	 - Firing rate of group -> continuous distribution of activation over feature space
	 - Link between DFT and biology
 - Extension of basic DF model: two-layer field

#### Neural Activation -> Perception, Cognition, Behavior
- Tuning curve: spike rate vs. stimulus/parameter dimension
- Gaussian-like tuning curves very common
- ![[Pasted image 20210517153345.png]]
- Receptive field: range where the tuning curve differs from baseline
	- for spatially tuned sensory neurons
- Receptive field profile: structure of tuning curve in receptive field
- Neurons typically tuned along >1 dimension
- Tuning curves of neuron set scattered over input dimension
- How to decode activity:
	- WTA scheme: not robust against noise
		- not stable
		- ambiguous (1 spike rate :: 2 values (Gaussian))
	- Information is carried collectively
- Population coding: properties of events reflected by distribution of activation over population
- ![[Pasted image 20210517154021.png]]
- Distribution over A,B,C unique for each input value
- Naturally robust to noise due to numbers
- Experimental verification of population coding: Does it predict behavior more reliably than single neurons? Do all active neurons  impact behavior? :: Yes
##### Superior colliculus - Saccade Control
- Tuning along angular direction and amplitude
- Would expect clustering in one region - observed too
- A,B,C - Centers of blob that would give rise to saccade vectors A,B,C
- Do neurons on periphery of blob also matter?
	- Tested by anesthetizing periphery neurons then providing stimulus
- ![[Pasted image 20210517154549.png]]
	- b) A region anesthetized - output (ideally A) unaffected (!!)
	- c) A region anesthetized - output (ideally B) shifts towards D
- Hence, overall activation profile more important than strongest ones

##### Arm Movement
- Experiment: Need to move arm from center to 1 of 8 buttons equidistant from center
- Population vector constructed for each movement direction
	- Find preferred direction for each neuron
	- Measure response for required direction
	- Wight preferred direction vector by activity and sum
	- $w_i(M)=d_i(M)-b_i$
	- $d_i(M)$: spike rate of neuron $i$ for direction M
	- $b_i$: bias/baseline spike rate
	- $P(M)=\sum_iw_i(M)C_i$
	- $C_i$: Preferred direction vector of neuron $i$
- More active neurons contribute more etc.
- Pop. vector compared to actual arm movement
- If all neurons relevant => more neurons included, more accurate : observed 
- ![[Pasted image 20210517155952.png]]
	- a) Ideal tuning curves
	- b) Vectors of 8 possible movements
	- c) Vectors weighted by spike rate during movement
		- length: contribution

>Possibilities: Motor acts competition, multiple items in working memory etc.

### Continuous Activation Distributions from Neural Responses
- Bridge gap between biological neural populations and DFs
- Transition from set of discrete values to continuous distributions
- May seem straightforward but mathh rigorr grr
- Refer [[#Arm Movement]]
	- Each neuron stands for its preferred direction vector
	- Estimate is an activity weighted sum
- Lot of information lost when distribution reduced to one vector
	- Width and shape of distribution :: matter
		- Few neurons strongly overlapping (or) Many neurons moderately activated
	- Multimodal distributions of activity
		- Average could be an unimportant value 
- Time to construct DPA from tuning curves
- DPA provides direct link to DF models

#### Construction of DPAs from Gaussian Tuning Curves
- Estimate tuning curves of neurons
- Receptive field center estimated manually
	- Used as basis for more precise assessment
	- Smoothed with Gaussian filter
	- Center of mass of output used as center for Gaussian tuning curve of fixed width
	- ![[Pasted image 20210517183818.png]]
	- Exact shape of receptive field lost in this process
- DPA now constructed using this set of Gaussian tuning curves
	- Normalize firing rate
	- Tuning curve weighted by normalized firing rate and summed
	- ![[Pasted image 20210517184137.png]]
	- Green - normalized TCs of neurons
	- Black - firing rate from one experimental condition
	- Blue - weighted TCs
	- Red - Sum
>Equations:
> $f_i(x,y)=N([m_{x_i},m_{y_i}],\sigma^2)$
> $\tilde{r}_i(a,t)=\frac{r_i(a,t)-b_i}{r_{m_i}-b_i}$
> $u(x,y)=\frac{\sum_ir_i(a,t)f_i(x,y)}{\sum_if_i(x,y)}$
- Activation value for each position even if no neuron's center at that location
- ![[Pasted image 20210517185143.png]]
	- a) Stimuli location b) Receptive fields c) Constructed DPA d) DPA from one stimulus 
- ![[Pasted image 20210517185931.png]]
	- DPA from stimuli at different positions 
	- Activation peaks in DPA widened over time contrary to belief that response gets sharpened over time 
- Final normalization step
	- Divide weighted sum of tuning curves by unweighted sum of tuning curves
	- Some regions may be sampled more densely by neurons eg. center portion in TC figure above
	- Will result in high activation value purely due to numbers
	- Compensate for this
- Still need good sample size of neurons in field
- Goodness of DPA can be determined by comparing with actual DPA produced by stimuli

#### Constructing DPAs for Movement Preparation
- Move arm from center to 1 of 6 targets
	- Direction indicated by red LEDs
	- Priming by green LEDs on possible upcoming locations
	- Varying levels of certainty
	- ![[Pasted image 20210517191630.png]]
	- PS: Preparatory signal, RS: Response signal, MVT: Movement onset, PP: Preparatory period, RT: Reaction time
- Feature space: Direction of arm movement
- Tuning curves determined directly from neural responses
- Average firing rate obtained by averaging over all trials, with different PSs and over RT period
- Individual properties of tuning curve preserved (width etc.)
- Same procedure as above to construct DPA, with the final normalization step being a subtractive one instead of divisive
>Raw tuning curves:
>$\tilde{f}_i(x_k)=\langle r_i(x_k,t_{rtp})\rangle$
>Average is over trials. Real tuning curves obtained by normalizing to interval \[0,1]
>DPA:
>$u(x)=\sum_ir_i(a,t)f_i(x)-\sum_ir_i(a,t_{pre})f_i(x)$
>$a$: trial condition, $t$: time interval, $t_{pre}$: window before stimulus presentation
>Subtractive term is the normalization
- DPA only provides values for the 6 directions, not a continuous field
- Less smooth than Gaussian method from earlier, but actually more accurate
- Constructed DPAs show single peak for target locations => great
- ![[Pasted image 20210517193041.png]]
	- Priming signal certainty affects initial peak
	- More uncertainty => weaker activation
	- Peak formation after target signal
- Thus, population doesn't encode single value; contains additional aspects such as certainty of upcoming movement
- Shape of distribution <-> certainty of movement
- DPA can be used to describe time course of activity also, as can be seen above
- New trials: RTs higher/lower than median
	- Total activity larger in fast RT trials
	- Activity concentration higher in fast RT trials
	- DPAs <-> Reaction time (behavioral variable)
- DPA useful even if neurons don't form topographical map
	- Motor cortex doesn't have spatial field like vision but DPA works over behavioral variable field, hence results independent of physical arrangement of neurons

#### Lateral Interactions in Primary Visual Cortex
- Sustained activation <-> interaction within population
- Response to elementary vs. complex stimuli
- ![[Pasted image 20210522123235.png]]
	- b) Constructed DPA for complex stimuli (solid) vs. superposition of DPAs for elementary stimuli (dashed)
		- Repulsion of peaks in distant case
	- c) Calculated time course of activation
	- d) Time course of activation from DF model
- Deviation from superposition => existence of interactions
	- Composite almost always weaker than superposition of elementary
	- During early part of stimulation for nearby case, activation higher in composite case though; also died down faster
- ![[Pasted image 20210522123819.png]]

#### Modeling Interaction Effects with DFs
- Lateral interaction -> strengthen similar neurons
- Same as peak formation and sustenance mechanism in DFT
- New Model:
	- Separation of field into exc. and inh. layers
	- Can account for repulsion effect
		- More inhibition on one side than another in bimodal case => drift apart

#### Two-Layer DFs
- Dale's law: Neurons emit same set of neurotransmitters at all their synapses
	- Very few exceptions
- Implications:
	- A neuron can only have one effect on another single neuron at all times
	- Inhibition has a delay => initial overshoot of excitation
- Two-layer field structure:
	- ![[Pasted image 20210522130447.png]]
	- Only excitatory receives external input
	- topological projections
	- no lateral interaction within inhibitory layer
	- Inhibition AoE wider if kernel sizes for exc-exc exc-inh and inh-exc are same (2x spreading)
	- To simplify: exc-inh kernel point-like (no spreading) and inh-exc kernel 2x wider
- For some configurations, 2-layer DF can act as oscillator
	- Can be nullified by using different time constants
- Selection decisions also possible
- Equations:
	- Activation of exc. layer: $u$
	- Activation of inh. layer: $v$
	- Kernels: $k_{uu},k_{uv},k_{vu}$
		- First letter target, second origin
	- $\tau_u\dot{u}(x,t)=-u(x,t)+h_u+s(x,t)+ \int k_{uu}(x-x')g(u(x',t))dx'-\int k_{uv}(x-x')g(v(x',t))dx'$
	- $\tau_v\dot{v}(x,t)=-v(x,t)+h_v+s(x,t)+ \int k_{vu}(x-x')g(u(x',t))dx'$
	- $k_{uu}(x-x')=c_{uu}N(x',\sigma_{uu}^2)$
	- For point-to-point connection from $u$ to $v$:
		- $k_{vu}(x-x')=\delta(x-x')$

#### Fitting Neural Data for Movement Preparation with DFs
- Single inhibitory node
- cf. [[#Constructing DPAs for Movement Preparation]]
- Activation profile broader for more pre-cued locations but also flatter due to inhibitory normalization

#### Relationship between DPAs, DFs and Neural Populations
- DPA: firing rates <-> continuous activation distribution
	- Does not explain emergence/evolution of activation patterns
	- Can only be determined for parameter spaced for which tuning curves are measured
	- Choosing inappropriate feature space can lead to misleading results
- DF: Generative models, linked with biological data
	- Makes predictions about activation patterns
	- Do not attempt to fully explain activation pattern of a single population, only that which is relevant to a single task
	
Can stability be retained as a property of neural processing while still representing high-dimensional information?
[[Hopfield Network]]

---

## Chapter 4: Embodied Neural Dynamics
- How does closing sensory motor loop affect neural dynamics
	- Creates behavioral dynamics
	- Not the same as activation variables
	- emergence of decisionsn from environment conditions

### Behavioral DYnamics in a [[Braitenberg Vehicle]]
- Sensors, effectors, body linking the two mechanically, nervous system linking to two though activation variables
- Situated in structured environment
- Taxis vehicle
	- ![[Pasted image 20210602084435.png]]
	- Activation plays limited role, only a transducer
	- Moves towards stimulus by using difference in intensity as control variables
- Goal: formalize dynamics of this vehicle
	- Function emerges from behavioral dynamics
	- Stability determines the functions that emerge
- ![[Pasted image 20210602091914.png]]
- Compose the functions relating intensity difference, activation, turning rate to directly obtain difference in turning rates as function of heading direction
- Turning rate is time derivative of heading
	- $\dot{\phi}=f(\phi)$
	- Behavioral dynamics
		- Abstract concept - removes details of mechanisms of sensory and effector systems
- Attractor state:
	- ![[Pasted image 20210602092500.png]]
	- Only relative orientation matters, absolute coordinate system doesn't
- Does not account for average turning rate which causes forward motion
	- Changing intensity profile leads to changing behavioral dynamics
- Bimodal system:
	- ![[Pasted image 20210602094213.png]]
	- Bistability leads to a selection decision
	- Self-stabilization of decision
	- Sensory input no longer uniquely determines behavior, depends on internal state also
	- Similar to bistability in neural dynamics
- Sources close together:
	- ![[Pasted image 20210602094545.png]]
- Bifurcation diagram: Pitchfork
	- ![[Pasted image 20210602094715.png]]
- DIfference between behavioral dynamics and cybernetics
	- In cybernetics, the input signal is an error/deviation from a goal or 'set point'
	- Similar to classical control theory, but unclear how to analyze in case of multiple sources
	- Formalizing as behavioral dynamics makes explicit the role of environment
	
###  Linking DFs to Behavioral Dynamics
- Additional decisions to withstand distraction -> inner state cairables
- Phonotaxis vehicle:
	- ![[Pasted image 20210607114519.png]]
	- 5 mics 45 dgrees apart
	- 60 degree sensitivty cone per mic
	- ![[Pasted image 20210607114634.png]]
		- Top - Weighted sum of tuning curves
		- Middle - Weighted tuning curves
		- Bottom - Sensitivity cones
- Limitations of using just mic inputs
	- Intensity variation of source (eg. music)
	- Other ambient sources -> apparent direction changes
- Use activation fields instead, with mic inputs as sensory inputs
	- Inputs are fixed to vehicle axis, not world axis
	- Need to account for this continuous change of coordinates
	- $\psi_i=\zeta_i+\phi$
	- $\psi_i$ - World coordinates
	-	$\zeta_i$ - Vehicle coordinates
	-	Solve by integrating behavioral dynamics equation
	-	No error correction in world frame -> doesn't matter as it is canceled by the motor command projection
-	Neural dynamics driven directly by sensors:
	-	![[Pasted image 20210607120349.png]]
	-	Volume gradually increased; detection decision shown
	-	Detection instability at critical source strength
-	Selection in presence of 2 sources
	-	![[Pasted image 20210607121048.png]]
-	1 source with reflecting surface on flank (robust estimation)
	-	![[Pasted image 20210607121201.png]]
-	Tracking of moving source
	-	![[Pasted image 20210607121227.png]]
-	To generate source-seeking motion
	-	induce attractor ins dyanmics of headin direction at location of snesory peak
-	First shot formalism: treat peak as mean of sensory distribution (with sigmoid applied to it)
	-	Requires normalization
	-	No peak -> computationally unstable
	-	Bad
- Activation field must generate attractor if peak, no change if no peak
	- use negative slope of dynamic contribution that erects attractor at peak location proportional to strength of peak
	- $\dot{\phi}=-[\int g(u(\psi))d\psi](\phi-\psi_{peak})$
	- $g$ - sigmoid
	- ![[Pasted image 20210607123203.png]]
	- Substituting the expression of mean of $\psi$, normalized:
	- $\dot{\phi}=-[\int g(u(\psi))\phi d\psi-\int g(u(\psi))\psi d\psi]$
	- Normalization cancels out, no divide-by-zero problems
	- Activation field -> heading dynamics
	- Vote $-[\phi-\psi]$ by each field location with strength proportional to $g(u(\psi))$
	- Range limiting factor may be used, cf. [[Dynamic Field Theory#Obstacle Avoidance]]
- Two sources -> decision instability, stabilization by neural field
- ![[Pasted image 20210607123910.png]]
	- Closer to left originally
- ![[Pasted image 20210607123937.png]]
	- Closer to right originally
- NOTE: Only vehicle coordinates matter here due to the nature of the equations
	- Errors in $\phi$ and $\psi$ cancel out
- Limb movement based on motor plans
	- ![[Pasted image 20210607124157.png]]
	- Muscles produce exactly enough torque to compensate for external weight
	- Reflex loops stabilize torque output
	- Movement -> shifting equilibrium point by the descending command <-> peaks setting attractors

---
#### Obstacle Avoidance
- Potential field approach
	-  Effector -> attractor 
	- Obstacles -> repellors
- Attractor dynamics approach
	- System is always in or near attractor
	- Direction of obstacle $\psi_{obst}$ generates a repelling 'forcelet'
		- $\dot{\phi}=...+(\phi-\psi_{obst})exp[-\frac{(\phi-\psi_{obst})^2}{2\Delta^2}]$
		- ![[Pasted image 20210607122213.png]]
		- Limited range
		- Two half-attractors
- Describes human obstacle avoidance quite well too
---

### Embodied A Not B
-  Neural dynamics to control real body acting in the world
-  Video input
-  Color matching filter -> only one color activates
-  ![[Pasted image 20210607144222.png]]
-  Same motor organization as phonotaxis vehicle
	-  Seeks yellow sources
-  Added memory trace cf. [[Dynamic Field Theory#Memory Trace]]
-  ![[Pasted image 20210607144420.png]]
-  Activation field and memory trace evolution:
	-  ![[Pasted image 20210607144803.png]]
	-  Boost at A due to specific cue, causes slight favoring later => peak
	-  Activation field at this time:
	-  ![[Pasted image 20210607144932.png]]
-  By the first B trial, significant memory of A => A-not-B error
-  Explanation for [[Dynamic Field Theory#Illustration DFT Model of Perseverative Reaching]]
-  Further experiments:
-  Obstacles in path to yellow target
	-  ![[Pasted image 20210607145347.png]]
	-  Left - without memory trace; Right - with memory trace
	-  'Young' (dotted line) robot makes error
		-  unable to sustain peaks of activation
	-  'Old' (solid line) robot retains memory of target
		-  can sustain peaks of activation

	-  Capacity to sustain peaks important to reach goal under broader circumstances
	-  With trace, both equivalent => peak stabilization
	- Memory trace- not as flexible as sustained activation
	- New peak can override previous target
	- Memory trace only forms from experience
- Why do younger ones rely on memory trace instead of sustained activation? [[Ideas+Thoughts]]
	- Not really known, maybe one is more complex
---

# Integrating Lower-Level Perception-Action with Higher-Level Cognition
- Does DFT scale up to higher-level cognition?
- Large scale theory of visual cognition?

## Chapter 5: Integration and Selection in Multidimensional Dynamic Fields

- Multidimensional fields enable integration of colors and spatial positions
	- Computationally costly
	- Full representation requires more neurons than brain has => implausible
- Fix: Selection
	- System can selectively "attend" to particular aspects

### Neurophysiology of Higher Dimensional Representations
- Neural populations for vision span 2D space of locations
- 'Simple neurons' - encode 2D location + orientation
	- Form basis of shape and motion perception
- Similar maps exist for other visual features: color, spatial frequency, ocular dominance etc.
	- All form representations over 2 space dims + 1 feature dim
- DF model -> activation over this 3d space
- How do we know the functional dimensions?
	- Vary particular perceptual dimensions and see which affect responses
- Multidimensional representations costlier than separate low dimensional repss


### Dynamics of Higher Dimensional Fields
#### Lateral Interactions in Multidimensional Fields
- $\tau\dot{u}(x)=-u(x)+h+s(x)+ \int k(x-x')g(u(x'))dx'$
- $x\in F$ - multidimensional field
- $k(x,y)$ - difference of Gaussians (exc and inh)
- $s(x,y)$ - Gaussian centered at input location
- ![[Pasted image 20210609123110.png]]

- Similar behavior to 1D case (mostly)
	- short range exc, long range inh, self stabilized peaks etc.
- Qualitatively different dimensions - different behavior
	- eg. spatial distance, angular orientation

### Real-time Integration and Selection in DFs
- 1 space dim + 1 hue dim
- ![[Pasted image 20210609124314.png]]
- Early visual cortex -> no global competition
- Read-out -> integrate over the disregarded dimension + convolve with Gaussian kernel
	- Input for 1D fields in figure
	- Loss of info -> location-color matching
- Integration not always useful -> spatial information needs to be conserved perfectly (selection) -> reaching behaviors
- How to get integration adn selection 
	- easy fix - force fields to have only one peaks
	- can select one at a time to avoid binding errors
- ![[Pasted image 20210609130118.png]]
	- Projection from 1D -> 2D field
- ![[Pasted image 20210609130452.png]]
	- a - stimulation of 2D field, projects forward
	- b - global boost of 2D from 1D to form peak
- ![[Pasted image 20210609130717.png]]
	- Local top-down influence
	- "Look for blue item" by boosting
	- Strengthens corresponding peak
	- Similarly for "Look for item on left" etc.
- Disadvantage 
	- may be looking for red object, but none present
	- multiple object might match
	- depends on detailed settings in such cases

### Integration & Selection in Autonomous Visual Exploratory Systems
- Close the loop on perception and action to create autonomous view of visual system
- Human visual system
	- rods cones distribution on retina uneven
	- concentrated at fovea (center)
	- saccade to bring attention to fovea
- biased competition model
	- how does visual working memory (VWM) interact with attention and early visual processing; influence saccades
- Two stream hypothesis
	- 'where' and 'what' streams of processing
	- spatial location vs. image features
- ![[Pasted image 20210610110835.png]]
	-  c, e - attention fields
	-  d - color memory field
	-  f - saccade motor field
-  Spatial field - WTA mechanism as before
	-  spatial attention
	-  logarithmic scaling of spatial dimension -> area near fovea contributes more
-  Saccade motor system -> strong local exc, global inh
-  Amplitude of saccade -> position of peak
	-  Neural integrator that integrates entire saccade field as inhibitor, to end saccade

### VWM  and Saccade Orienting in Remote Distractor
- ![[Pasted image 20210610112140.png]]
	- Memorize color (blue box)
	- Perform saccade to red spot (bigger, farther), avoid green spot (smaller, closer distractor)
	- Test memory of color by identifying box
	- Some trials had different saccade dots with color matches as shown on right
- ![[Pasted image 20210610112528.png]]
	- Even though distractor was always on wrong side, errors still made when color matched
	- When distractor color matched, ~50% error
	- When target color matched, ~0% error
- Simulations of this experiment
	- ![[Pasted image 20210610113207.png]]
	- Distractor color matching strengthens extant peak in color memory field
	- Causes back projection to sensory field and then spatial field, that makes it peak at the distractor position
	- Wrong saccade
- Activation bimodal in all conditions

### Function and Fallibility of Visual Feature Integration
- Should this framework be expanded to higher dimensions?
	- Not really, since the visual cortex doesn't do this
- Brain has separate populations for each dimensions -> less computationally expensive
- But then how do we see objects as wholes instead of separate features -> binding problem
- Expanded biased competition model -> add more fields and achieve same functionality without dramatic increase in demands
- ![[Pasted image 20210610115021.png]]
	- top b, c, d - color field
	- bottom b, c, d - shape field
	- b - visual sensory fields
	- c - feature attention fields
	- d - feature memory fields
	- e - spatial attention field
	- f - spatial read-out field (formerly saccade motor field)
- Only one extra set of fields here but can have more
- Space-color (S-C) fields and space-shape (S-S) fields
- Both visual sensory fields are coupled with spatial attention field -> coupled to each other indirectly 
	- (b<->e<->b)
- Single multifeature item -> peak in S-C field + peak in S-S field
- Multiple items -> good old which-is-which problem
	- Forcing selection (single peak) helps here too
	- Single peak in both fields must correspond to same item
	- Coherent representation
	- Need mechanism to determine which is chosen
- Color attention and shape retrieval task:
	- Multiple objects (letters) in different colors shown
	- Asked to say which had which color: "which letter was in red"
- Model adjustments:
	- Cue item presented at start, having the required feature (color) -> peak  in memory field
	- Read-out field -> maintain single peak (spatial attention)
- Simulation of model:
	- ![[Pasted image 20210610122538.png]]
	- a - cue item presented (not shown in figure)
	- b - color memory peak at one value corresponding to cue item -> ridge in S-C field -> peak in spatial attention field
	- c - S-S peak of target item prevails
	- d - illusory conjunction due to a nearby distractor enhanced too much by ridge; location response in between the two letters
	- With location cue, independent selection of shape and color observed in experiment
	- With color cue, dependent selection of shape and location
	- After location selected, doesn't matter how it was arrived at, for the other one-of-two decisions to be made
- Failure of model -> precisely in the same way that humans fail
	- Feature errors (unpresented features reported as being seen)
	- Illusory conjunctions (red X + green T -> green X, etc.)
		- Seen above, ridge movement due to reciprocal coupling
		- Probability higher for smaller inter-item distance
	- Another IC experiment - participants shown multiple letters; one always green; asked to pick location of green O even when there was none; picked average spatial location of green letter and O
		- Similar behavior found in model
	- 2 causes for ICs - spatial proximity and feature similarity -> influence each other, elevating IC probability
- Location Uncertainty Theory
	- Uncertainty of position in feature registration phase causes errors
	- Not needed in this model; ICs generated at attention mechanism (feature integration) level
---

## Chapter 6: Integrating Perception and Working Memory in a Three-Layer Dynamic Field Model
- Spatial recall and change detection
- ![[Pasted image 20210611135831.png]]
- Common feature-  maintain stable state
	- spatial reference frame and comparison
- Integration of perception and working memory

### integrating perceptual and memory processes in 3-layer NF architecture
- 3-layer field
- ![[Pasted image 20210611140501.png]]
- contrast field $CON(u)$
- working memory field $WM(w)$
- inh field $Inhib(v)$
- WM to CON only through INH
- CON direct input

### Spatial recall biases
- Repelling of WM peak away from midline peak in CON
	- angular error
	- varies across trials
- Complex pattern of drift and variability

### Visual Change Detection
- ![[Pasted image 20210611141709.png]]
	- left - no-change test set
	- right - change test set
	- encoding, maintenance over delay, generation of response, decision response
- Peaks below baseline after inputs removed, in CON
- peaks remain in WM
- Excitatory layers of all 3 coupled to accumulator to generate decision

### Behavioral Signatures of the 3 Layers
- How to use model to address behavioral phenomena

#### Encoding
- Rate of encoding in WM increases as no. of items
- ![[Pasted image 20210611154558.png]]
	- set size

#### Maintenance
- Midline repulsion of peaks
	- Strength of midline peak varied in experiment by marking / not marking
- Predictions
	- toward axis -> better discrimination
	- near axis -> enhanced discrimination
	- salience of axis -> more enhancement
- ![[Pasted image 20210611155018.png]]
	- Mistake when second stimulus presented away from axis (in direction of drift)
- Other two predictions also verified in experiments
- Peak repulsion -> strong inhibition -> similar items held nearby recalled to be more different than they really are
- ![[Pasted image 20210611155454.png]]
	- Color wheel test -> two similar colors recalled in opposite directions

#### Comparison
- Change detection should be enhanced with multiple similar items vs. few unique items
	- Confirmed in experiment
	- ![[Pasted image 20210611160144.png]]
- Capacity limited model
	- Inhibition overwhelms beyond a point

#### Decision
- Limitations of old single threshold (same / different) model
	- No active decision in 'different' trial
	- Not neurally realistic -> relies on absence of activation
- Both fixed here (two threshold variables, active decisions)
- Faster response on 'same' trials

### Comparison with Other Models
- Category Adjustment Model
	- Fine location + category : encoding
	- Less broad in explanation scope than DFT 3-layer
- Fixed resolution slots model
	- WM stores info in limited discrete slows
	- When set size exceeds slot count, performance degrades
- Another similar: flexible allocation of WM space
- DFT better than these two:
	- Metric effects can be explained
	- Variety of tasks
---

## Chapter 7: Sensory-Motor and Cognitive Transformation
- Reference Frames

### Role of Reference Frames
- ![[Pasted image 20210621150309.png]]
- Representation by population in one frame is consistent -> inconsistent in others moved relative to this
- Reference frame of neural population -> independent of anatomical (retinotopic) organization of individual neurons

### Reference Frame Transformations - Gain Modulation
- Variable shift parameterized by current position of eyes
- Gain-modulated neurons
- Fixation task while visual stimuli presented
	- ![[Pasted image 20210621163439.png]]
- Firing pattern consistent with retinocentric representation
- Overall strength depended on fixation point (gaze), though
- ![[Pasted image 20210621163556.png]]
	- Typically linear dependence on gaze direction

### Reference Frame Transformations - DF Model
- retinocentric -> body centered 
- need to perform angular addition with neural population
- ![[Pasted image 20210622155040.png]]
	- all points on diagonal correspond to same real-world point
- retinal position + gaze direction -> body-centered location

### Extensions of the Basic Mechanism
- ![[Pasted image 20210622155051.png]]
- Need support for multiple peaks
- Reversal of projection direction -> memory of visual location
- ![[Pasted image 20210622155338.png]]
- Reference Frame Alignment problem:
	- ![[Pasted image 20210622155445.png]]
	- ![[Pasted image 20210622155604.png]]
	- Strongest input location will determine correct shift
	- Symmetric arrangement of boxes -> impossible to determine correct orientation
		- Single gaze peak makes sense

### Multidirectional Transformations
- Two-way connections between all 3 fields
- Strength of activation determines direction of signal flow
- ![[Pasted image 20210622161222.png]]
- Essentially one large dynamical system

---

## Chapter 8: Integrating What and Where

