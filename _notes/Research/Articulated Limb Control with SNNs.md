[[Research]] [[Neuromorphic]]

# Controlling Articulated Robots in Task-Space with Spiking Silicon Neurons

[[Kwabena Boahen]]

![Pasted image 20210615124840.png](Pasted%20image%2020210615124840.png)

## Task Space Control
- Operational space framework
	- user provides desired forces $f^*_x$
	- task forces projected into joint torques; gravity compensation added
	- $\Gamma = J^T_xf^*_x+\Gamma_g*$
	- $\Gamma_g=-\sum_0^4m_iJ^T_{com_i}g$
		- $m_i$ - link masses
		- $J^T_{com}$ - CoM Jacobians
- Provides closed form time-invariant function that linearizes dynamics

### Factorization
- Dimensionality reduction
- Nonlinear sub-functions over 3 out of 6 dimensions
	- Cubic sample size
	- eg. $f=(x+y)z = xz + yz$ : 3D function -> 2 2D functions
- Composition avoided as more layers are needed
	- Delays
- Five pools -> represent 3 variables

- ![Pasted image 20210615125610.png](Pasted%20image%2020210615125610.png)

- $\Gamma = J^T_xf^*_x+\Gamma_g*$
- $J_x = [J_{x,0}\;J_{x,1}\;J_{x,2}]$
- $J_{x,0}^T = [sin(q_0)(-0.35cos(q_2)+0.225sin(q_1))\;\;cos(q_0)(0.35cos(q_2)-0.225sin(q_1))\;\;0]$
- $J_{x,1}^T = [-0.225cos(q_0)cos(q_1))\;\;-0.225cos(q_1)sin(q_0))\;\;-0.225sin(q_1)]$
- $J_{x,2}^T = [-0.35cos(q_0)sin(q_2))\;\;-0.35sin(q_0)sin(q_2))\;\;-0.35cos(q_2)]$
- $\Gamma_g^T=[0\;\;1.026sin(q_1)\;\;1.612cos(q_2)]$
- Each term function  of 3 or fewer inputs
- ![Pasted image 20210615133754.png](Pasted%20image%2020210615133754.png)


### Regression
- Encoding vectors chosen using L1 basis pursuit
- Restricted joint angles and forces according to robot operating range
- Decoding weights: $d=argmin_d\;||Ad-y||_2+\lambda||d||_2$
- Responses of the 5 3D pools:
- ![Pasted image 20210615130118.png](Pasted%20image%2020210615130118.png)


### Programming
- MxN weights for decoding M sub-functions from N neurons
- Stochastic spike distribution: if $i$ spikes, look at $w_{ij}$, generate random number $r_j$, if $r_j<w_{ij}$, send spike to neuron j
	- Average spike rate will then be $\sum a_i w_{ij}$ 
- Output spike trains converted with exponential filters into command signals

## Characterization
- Random reaching task, without zeroing

### Reaching and Drawing
- PD control law for force trajectories
- $f^*_x=k^T_p(x_{des}(t)-x_{curr})-k^T_v\dot{x}_{curr}$
- Remains stable during ~5cm perturbations

### Increasing Performance
- Better with more neurons
- ![Pasted image 20210615131251.png](Pasted%20image%2020210615131251.png)
- Lack of inertial model is a constraint
	- forced to use conservative values for proportional gains, with over-damping
	- reduces ability to overcome anisotropic friction
	- abrupt gravity torque changes

## Conclusion
- 1280/1mil neurons used
	- 800 robots simultaneously?
	- 4mW/robot

- Challenges [[Ideas+Thoughts]]
	- Mapping algorithms that compute task-space inertias to decouple task-control from robot dynamics
		- Quadratic form over CoM Jacobian
	- Simultaneous control of force and torque for arbitrary surface contact
		- Functions over groups of rotations (non-commutative)
	- Multiple simultaneous control tasks
		- projecting one task into acceleration null space of another
		- Jacobian's inertia regularized generalized inverse
