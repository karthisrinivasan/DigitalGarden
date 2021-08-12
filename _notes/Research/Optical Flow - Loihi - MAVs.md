# Neuromorphic control for optic-flow-based landings of MAVs using the Loihi processor
- [[Neuromorphic]] [[Research]]
## Introduction
- Providing Micro Air Vehicles (MAVs) autonomy requires many sensors + redundancy + computation
- Insects great at this
- Optic flow - brightness change in retina due to observer's relative motion
- [[Loihi - Survey of Results]] chip - fully embedded application - 1st
- ![Pasted image 20210515185039.png](Pasted%20image%2020210515185039.png)
- Ventral optic flow divergence -> Thrust setpoint for smooth landing
- ![Pasted image 20210515185207.png](Pasted%20image%2020210515185207.png)

## Materials and  Methods
#### Vertical Landing with Optical Flow Divergence
- Camera with optical axis orthogonal to static planar scene
- Moving camera => divergence => ratio of axial velocity ($V$) to distance $h$ from surface
	- $D=V/h$
- Estimate of D from relative temporal variation in distance between tracked corner-pairs:
	- $\hat{D}(t)=\frac{1}{N_D}\sum^{N_D}_{i=1}\frac{1}{\Delta t}\frac{l_i(t)-l_i(t-\Delta t)}{l_i(t-\Delta t)}$
	- $N_D$: No. of pairs
	- $l_i(t)$: Distance between pair of tracked corners
- Smooth landing via constant divergence during approach
- Desired divergence: $D_{sp}=1s^{-1}$

#### SNN
Simulation:
- Standard LIF Model
- ![Pasted image 20210515191112.png](Pasted%20image%2020210515191112.png)
- 'Position coding' : Each value of $\hat{D}(t)-D_{sp}$ -> 1 of 20 buckets -> triggers single spike
- Cubical tuning curves
- Decoding to continuous $T_{sp}$
	- Spike trace: $X_i(t)=\tau_{x_i}X_i(t-\Delta  t)+\alpha_{x_i}s_i(t)$
	- Thrust setpoint: weighted average of thrust vector $\bar{q}=(-0.4,-0.2,0,0.2,0.4)$
	- $T_{sp}(t)=\frac{\sum_iq_iX_i(t)}{\sum_iX_i(t)}$

Loihi:
- Current-Based (CUBA) LIF Model

Evolutionary Optimization:
- Fitness = Accumulated divergence error
	- $\sum_t|\hat{D}(t)-D_{sp}|$
	- averaged over landings from different heights
- Varying sources of noise => close reality gap

## Results
- 4 randomly initialized evolutions of 200 generations
- Only z-dimension controlled by Loihi
	- (x,y) controlled through OptiTrack motion capture system
- PySNN simulation and on-chip networks exhibit no significant differences
- ![Pasted image 20210515202619.png](Pasted%20image%2020210515202619.png)
- ![Pasted image 20210515202824.png](Pasted%20image%2020210515202824.png)
#### Real-World Landings
- ![Pasted image 20210515203025.png](Pasted%20image%2020210515203025.png)
- ![Pasted image 20210515203033.png](Pasted%20image%2020210515203033.png)
