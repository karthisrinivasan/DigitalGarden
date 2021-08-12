[[Research]] [[Neuromorphic]] [[MITACS Project]]

# An Adaptive Spiking Neural Controller for Flapping Insect-scale Robots

Taylor Clawson [[Terrence Stewart]] [[Chris Eliasmith]]

## Introduction
- Insect robot controller - robust to wing asymmetries
- Actuator dynamics variation
- Need to stabilize fast unstable dynamic modes
- Periodic nature -> limit cycles instead of equilibrium points
	- Time-variant systems
- 12 degrees of freedom but only 3/4 control inputs
- RoboBee 
	- 20mW power budget, most for actuators
	- Insufficient rotational damping -> open loop hovering is unstable
	- Need controller robust to uncertainties in physical parameters prior to learning
	- Portion of SNN control turned offline to approximate linear controller

## Dynamic Model
- ![Pasted image 20210608115618.png](Pasted%20image%2020210608115618.png)
- Only stroke angle can be controlled directly
- Wing pitch cannot be controlled during flight
- ![Pasted image 20210608120132.png](Pasted%20image%2020210608120132.png)
	- Roll control -> relative amplitude
	- Pitch control -> mean stroke angle
- Instability -> net drag above CoM
	- pitch and toll
	- yaw neutrally stable so not considered
- Rigid body dynamics + blade element theory -> 6 degrees of freedom
- $q= [\phi_R\;\phi_L\;\psi_R\;\psi_L\;\phi\;\theta\;\psi\;x\;y\;z]^T$
	- Stroke angles, Pitch angles, Body Euler angles, body position
- State: $x(t)=[q(t)\;\dot{q}(t)]^T$
- Control vector: $u=[u_a\;u_p\;u_r]$
	- Amplitude, pitch bias, roll bias
- Equation of motion:
	- $M(q)\ddot{q}+C(q,\dot{q})=B(t)u$
	- $M$ - Inertia matrix
	- $C$ - Nonlinear forces
	- $B$ - Input matrix
- Control affine form:
	- $\dot{x}(t)=f(x)+G(x,t)u(t)$
- Linearization about a periodic trajectory -> good approximation for small deviations from hovering
- Steady state hovering trajectory: $x^*(t)$ with period $T$ = 120Hz 
- State deviation: $\tilde{x}(t)=x(t)-x^*(t)$
- Control deviation - similar definition
- $\tilde{x}(t)=A(t)\tilde{x}+B(t)\tilde{u}$
	- Normal linearization of dynamics
	- $A$ and $B$ have period $T$
- Inaccurate for transient response; for all control inputs
- Eg. step change in roll input $u_r$
	- Causes primarily rolling
	- Left amplitude > right amplitude
	- ![Pasted image 20210608123318.png](Pasted%20image%2020210608123318.png)
	- $B$ significantly affected due to yaw torque
		- a - linearized transient response calculation
		- b - equilibrium trajectory for body, linearization for wing
	- Yaw remains, but yawing torque cancels if input held constant

## SNN Control Design
- 4 populations for the two terms
	- Approximation of linear controller _ adaptive term for parameter variations
	- 800neurons total
- Linear Proportional Integral Filter (PIF) compensator
	- Augmented state vector $\chi(t)=[\tilde{x}^T(t) \;\tilde{u}^T(t)\; \eta^T(t)]$
	- Constant gain matrix $K$
	- $\eta(t)=\eta(0)+\int_o^ty(\tau)d\tau$: integral of output error
	- Control law: $u_{PIF}(t)=\int_0^t-K_{\chi}(\tau )d\tau$
	- Control input error and integral of output error assumed zero for SNN approximation
	- state error most significant term
- State encoded as spike sequences in population - NEF
	- $r_i=G_i(J_i(x),t)$
	- $J_i(x)=\alpha_ie_i^Tx(t)+J_i^{bias}$
		- $e_i$ - preferred direction vector
- LIF model with Neural Engineering Framework
	- Exponential post-synaptic filter: $h_i(t)=Ke^{-t/\tau}$
	- Activity: $a_i(x,t)=\sum_kh_i(t-t_{ik})$
	- Linear decoders to obtain control signal - $u_0(t)=\sum_ia_i(x,t)d_i$
	- Decoders obtained from least-squares over sampled data-set - $d_i = argmin_{m_i}\int_x||g(x)-\sum_i\bar{a}_i(x)m_i||^2dx$
		- $g$ - output of PIF for given point in state space
		- $\bar{a}$ - time averaged neuron activity in steady state for same point
	- $u_0(t)$ closely approximates PIF compensator signal
	- Not sufficient, need a $u_{adapt}(t)$ signal to help out
- $u_{adapt}(t)=[u_a(t)\;u_p(t)\;u_r(t)]$
- Each from separate population of neurons
- ![[Pasted image 20210608130708.png]]
- Each population trained online to zero the error signal:
	- $E(t)=\Lambda^T(\Delta x(t)+\alpha\Delta\dot{x}(t))$
	- Inner product between state error and constant vector
- Assumption: Actuator performance dominates variations in body dynamics in z direction so $u_a(t)$ not computed from state; rather from activity
	- $u_a(t)=\sum_ia_{a,i}(t)d_{a,i}(t)$
	- $a_{a,i}=h_i(t)*G_i(J_i^{bias},t)$
	- Decoders updated based on adaptation rate $\gamma$:
		- $\dot{d}_a(t)=\gamma a_a(t)E(t)$
		- $a_a(t)= [a_{a,1},a_{a,2}...a_{a,N}]^T$
	- $\Lambda$ chosen so that error depends on only z velocity and its derivative
- $u_p(t)$,$u_r(t)$: depend on state
	- $u_p(t)=a_p^T(x,t)d_p(t)$
	- $\dot{d}_p(t)=\gamma a_p(x,t)E(t)$
		- $\Lambda$ chosen so that error only depends on x velocity and its derivative
	- $u_r(t)=a_r^T(x,t)d_r(t)$
	- $\dot{d}_r(t)=\gamma a_r(x,t)E(t)$
		- $\Lambda$ chosen so that error only depends on y velocity and its derivative
- Adaptive amplitude -> zero out any error in body z velocity; the pitch input -> zero out error in the body x velocity; roll input -> zero out the error in body y velocity
- $u(t)=u_0(t)+u_{adapt}(t)$
	- $u_0(t)$ - offline training
	- $u_{adapt}(t)$ - online training

## Results
- Wing asymmetry
	- Static amplitude bias between L,R for roll
	- Stroke angle offset for pitch
- PIF Compensator
	- ![Pasted image 20210608132434.png](Pasted%20image%2020210608132434.png)
	- ![Pasted image 20210608132511.png](Pasted%20image%2020210608132511.png)
	- Yaw unstabilized, x,y velocities slow stabilization
	- In-plane rotation + position drift
- SNN Controller
	- Adaptive term tuned using grid parameter search
	- RoboBee remains within 10cm of starting position
	- ![Pasted image 20210608132856.png](Pasted%20image%2020210608132856.png)
	- ![Pasted image 20210608132905.png](Pasted%20image%2020210608132905.png)
	- No yaw control authority still, so no stabilization


