[[Research]] [[Analog]] [[Neuromorphic]]

# Current Mode Subthreshold MOS Circuits for Analog VLSI Neural Systems

[[Research/Kwabena Boahen]] 

## Subthreshold Device Operation
### Device Model
- $I_{ds}=I_0e^{(1-k)V_{bs}/V_T}e^{kV_{gs}/V_T}(1-e^{-V_{ds}/V_T}+V_{ds}/V_0)$
	- $I_o$: zero-bias current
	- $V_0$: Early voltage

## Current Mode Approach
- Signals as currents

### Translinear Principle
- Translinear - linear relationship between transconductance and current
- Closed loop of equal number of oppositely connected translinear elements:
	- Product of current densities in one direction = corresponding product in the other direction
- ![Pasted image 20210616145038.png](Pasted%20image%2020210616145038.png)
	- $I_WI_Z=I_XI_Y$
	- $I_W$ - normalization
	- Can be derived through: $V_1+V_2+V_3+V_4=0$
	- $(V_T/k)[ln(I_X/I_0)+ln(I_Y/I_0)-ln(I_W/I_0)-ln(I_Z/I_0)]=0$
	- Effectively a log-antilog block

### Current Conveyor
- 3-port device to replace opamps
- ![Pasted image 20210616145500.png](Pasted%20image%2020210616145500.png)
	- X follows changes at Y, conveyed to low-conductance node Z
- ![Pasted image 20210616145545.png](Pasted%20image%2020210616145545.png)
	- X follows largest Yi, turning of all others
	- Tail current I_X conveyed to Zi 
- ![Pasted image 20210616145711.png](Pasted%20image%2020210616145711.png)
	- Current controlled current conveyor
	- Potential at X determined by control current I_Y
	- IZ=IX, g(VX)=IY, g -> log for subthreshold, sqrt for superthreshold
	- If Z connected to supply -> basic trans-resistance amplifier
- ![Pasted image 20210616150650.png](Pasted%20image%2020210616150650.png)
	- fan-out of current input as voltage outputs
	- fan-in of current inputs

## System Applications
### Associative Memory
- Bidirectional junction for synapse
- ![Pasted image 20210616151028.png](Pasted%20image%2020210616151028.png)
- ![Pasted image 20210616151036.png](Pasted%20image%2020210616151036.png)
	- Turn on/off synapse by setting S to GND/VDD
	- $I_i$: sent signals
	- $\hat{I}_i$: received signals
	- Sent signals slightly perturbed by receive signals strength

###  Winner-Takes-All
- ![Pasted image 20210616151409.png](Pasted%20image%2020210616151409.png)
	- Inputs at Y, outputs at Z
	- Largest input takes all of the X current
- Each conveyor sees V_X at comm. node
- If smaller than maximum, M2 enters linear region, turning M1 off
- If two inputs are very similar, exponential conversion
	- $\frac{\Delta I_Z}{\Delta I_Y}=A\frac{I_Z}{I_Y}$
	- $\Delta I$: Difference between two similar currents

### Pyramidal Neurons
- ![Pasted image 20210616152020.png](Pasted%20image%2020210616152020.png)
	- $X_V$ ~ Apical dendrites; carries i/o signals
	- $X_L$ ~ basal dendrites; mediates lateral inhibition

### Silicon Vision
- ![Pasted image 20210616153613.png](Pasted%20image%2020210616153613.png)
- Laplacian filter "Mexican hat"
- Resistors -> gap junctions
- Top layer nodes -> receptors (R)
- Lower layer -> horizontal cells (H)
- Parasitic BJT to transduce light into current
- ![Pasted image 20210616154137.png](Pasted%20image%2020210616154137.png)