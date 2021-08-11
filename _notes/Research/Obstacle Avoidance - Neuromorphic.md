[[Neuromorphic]] [[Research]] 
## Obstacle Avoidance and Target Acquisition for Robot Navigation Using a Mixed Signal Analog/Digital Neuromorphic Processing System

- [[Giacomo Indiveri]] 
- Interfacing ROLLS (reconfigurable online learning) mixed-signal neuromorphic processor to DVS
- [[Dynamic Neural Fields]] for Target Acquisition

### Introduction
- Simple conceptual formulation for obstacle avoidance - [[Braitenberg Vehicle]]
- Mismatch is useful
- Population coding, recurrent connections
- Attractor Dynamics

### Materials and Methods
- Pushbot, ROLLS, Parallella computing board for control (optional in application scenarios => fully neuromorphic)
![[Pasted image 20210508232249.png]]
- Parallella - manages event stream between processor and robot

#### ROLLS
- 256 spiking neurons
- Fully connectable
- 256x256 programmable synapses; 256 learnable synapses
- No online learning used here
![[Pasted image 20210508233143.png]]
- 8 level weight quantization
- 4mW avg. power consumption

#### DVS
- Event vector $e=(x,y,ts,p)$
	- pixel location, time stamp, polarity (on/off event)
- AER Protocol for off-chip communications
- ~microseconds for off-chip data transfer
- Challenges: homogeneous surface, noise, low spatial resolution, limited FOV

#### Network Architecture
![[Pasted image 20210509010428.png]]
- A - Obstacle avoidance architecure
- B - Target acquisition structure
- OL/OR - Obstacle left/right - 16 neurons each
	- one spike per DVS event in left half
	- enough events => firing
- DL/DR - Drive left/right
	- OL => DR ; OR => DL
	- DL/DR mutual inhibition, WTA
	- stable decision
	- DL,DR inhibit OL,OR as many DVS events occur during turning
		- Suppress this noise
- Speed (SP) recevies input from constant firing EXC group
- EXC group: 
	- Constant firing from transient pulse
	- Sets constant speed in obstacle-free environment
	- Inhibited by OR/OL, reducing speed
- 96 neurons total
- Angular velocity $v_a$ and Forward velocity $v_f$
	- $v_a=c_{turn}(\frac{N^{spike}_{DL}}{N^{n}_{DL}}-\frac{N^{spike}_{DR}}{N^{n}_{DR}})$
	- $v_f=c_{speed}\frac{N^{spike}_{SP}}{N^{n}_{SP}}$
	- No. of spikes in a time window / No. of neurons in that population

#### [[Dynamic Neural Fields]] for Target Representation
- 128 neurons to represent targets
- events consistently from same column - firing
- WTA - noise and too large/too small object filtering
- Blinking LED - target
- 3 regions in population
	- left of midline
	- right of midline
	- central 16 neurons unconnected

#### Combining Avoidance and Acquisition
- ROLLS biases - obstacle contribution strength
- Connectivity matrix of programmable synapses
![[Pasted image 20210510015834.png]]

#### Single Obstacle
![[Pasted image 20210512091054.png]]
- Performance changes with speed, contrast of object

#### Two Obstacles
![[Pasted image 20210512091511.png]]
- Detect events that are clustered in time and space
- Around both safer than in between the two
- Adaptive connectivity depending on speed is feasible [[Ideas+Thoughts]]

#### Moving Obstacle
- More robust than static as it produces more DVS events
- ![[Pasted image 20210512091829.png]]

#### Cluttered Environment
- Limitations:
	- Narrow FOV
	- Limited contrast range
	- ![[Pasted image 20210512092016.png]]
	- Improvements:
		- 2 extra populations to suppress obstacle populations when robot is turning
		- Graded connections - obstacles in center of FOV - stronger activation

#### Behavior Variability
- Can be used as drive for exploration
- ![[Pasted image 20210512095514.png]]

#### Target Acquisition
- ![[Pasted image 20210512101055.png]]
- Chasing a moving target:
- ![[Pasted image 20210512101141.png]]


