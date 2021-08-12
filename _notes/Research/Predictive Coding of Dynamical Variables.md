[[Research]] [[Neuroscience]]

# Predictive Coding of Dynamical Variables in Balanced Spiking Networks

-	Two observations about the brain
	- Neural Responses highly variable
	- Level of received excitation/inhibition for a neuron is tightly balanced
- These are consequence of NNs that represent information efficiently in spikes
- Approach based on assumptions:
	- Info about the represented variables (dynamic variables here) can be linearly read out from spike trains
	- Spike is fired only if it improves representation of the variables
- Derive network of LIF neurons that can implement arbitrary linear dynamical systems
- Membrane voltage <-> prediction error about a common population level signal
- Balanced networks >> reliable than other population code models
- Spikes matter more than previously thought
- Cortical representation much higher than previously thought, possibly

## Introduction
- most research on attractor dynamics
	- State cars M0< inst firing rates
- Common assumption: random nature of spike trains averaged over large populations or longer time periods
- Properties of balanced networks: derived from single efficiency principle
- Procedure:
	- Starting assumption: encoded variables can be extracted by synaptic integration
	- Specify loss function
	- Neurons fire spike only if it decreases loss function
- Spike train variability is not noise
- Population acts as super-unit which tracks variable accurately

## Results
### Assumptions
- ![Pasted image 20210530192637.png](Pasted%20image%2020210530192637.png)
	- Blue inhibitory, Red excitatory, circle fast, diamond slow
- LDS of x:
	- $\dot{x}=Ax+c(t)$
	- $c(t)$: inputs/control variables
- Want to estimate $x(t)$ using a network of N neurons
- Spike trains: $o_i(t)=\sum_k\delta (t-t_i^k)$
- Assumption 1: Estimate is obtained using weighted leaky integration of spike trains
	- $\dot{\hat{x}}=-\lambda_d \hat{x}+\Gamma o(t)$
- Each spike contributes an exponentially decaying kernel -> simplified PSP
- Weights ($\Gamma_i$): Output kernel of neuron i
	- Columns of $\Gamma$
- In terms of firing rates:
	- $\dot{\hat{x}}=\frac{1}{\lambda}\Gamma r(t)$
	- $\dot{r}=-\lambda_d r+\lambda_d o(t)$
- Assumption 2: Network optimizes over spike times $t_i^k$, doesn't change the fixed output weights $\Gamma$
	- Decoding weights chosen a-priori
- Minimizes the cost function:
	- $E(t)=\int_o^t du(||x(u)-\hat{x}(u)||_2^2+\nu ||r(u)||_1+\mu ||r(u)||_2^2)$
	- Linear $r$ term forces network to use as few spikes as possible
	- Quadratic $r$ term forces network to distribute spikes more equally among neurons

### Network Dynamics
- Assume greedy minimization
- Gives rise to firing rule:
	- $V_i(t)>T_i$
	- $V_i(t)=\Gamma_i^T(x(t)-\hat{x}(t))-\mu\lambda_dr_i(t)$
		- Membrane Potential
	- $T_i=\frac{\nu\lambda_d+\mu\lambda_d^2+||\Gamma_i||^2}{2}$
		- Firing Threshold
	- In limit $\mu$->0, membrane potential is projection of prediction error onto output kernel
	- For finite $\mu$, penalized prediction error
- If neuron already has high firing rate, large error will be needed to increase it
- Governing differential equation:
	- $\dot{V}_i=-\lambda_VV_i+\sum_1^NW_{ik}*o_k(t)+\Gamma_i^Tc(t)+\sigma_v\eta(t)$
	- $W_{ik}(t)$: Weight matrix of connectivity filters
		- $W_{ik}(u)=\Omega_{ik}^sh_d(u)-\Omega_{ik}^f\delta(u)$
		- Fast connections: $\Omega^f=\Gamma^T\Gamma+\mu\lambda_d^2I$
		- Slow connections: $\Omega^s=\Gamma^T(A+\lambda_dI)\Gamma$
		- Diagonal elements of $\Omega^f$: self-connections -> implement reset after spike -> eq. to LIF
	- $\eta(t)$: Noise
- Slow/Fast - typically opposite effects
- Off-diagonal elements of $Omega^f$: competition among neurons
- Neurons with similar kernels inhibit, opposite kernels excite
- Slow connection: cooperation among similar neurons
	- Maintain persistent activity when x is static
- $PSP_{ik}(t)=W_{ik}*h_v(t)$
- $h_v(u)=\Theta(u)exp(-\lambda_vu)$
	- Integrate governing equation for single spike
- Example PSP:
	- ![Pasted image 20210531110618.png](Pasted%20image%2020210531110618.png)
- Some neurons inhibit, excite different targets -> violation of Dale's law -> can be fixed by creating separate cost functions; equivalent

### Scaling and Physical Units
- Mapping equations to real physical units
- $V_i'$->$a_iV_i/T_i+b_i$
- $T_i'$->$a_iT_i/T_i+b_i$
- Set $a_i,b_i$ so that $T_i'=a_i+b_i=-30mV$, $V_{i,reset}'=T_i'-a_i\Omega_{ii}^f/T_i=-80mV$
	- Unique solution for $a_i,b_i$
- Scaling with N (network size)
	- $\Gamma_i \sim 1/N$
	- $T_i \sim 1/N^2$
	- $W_{ik} \sim 1/N^2$
	- Hence $W_{ik}'$ does not scale
	- Detailed balance of excitatory/inhibitory maintained

### Sensory Integration and Tracking
- Consider LDS:
	- $\dot{x}=-\lambda_sx+c(t)$
	- Scalar x
- ![Pasted image 20210531110804.png](Pasted%20image%2020210531110804.png)
	- 400 neurons, 
	- half positive kernels -> fire when x increasing
	- half negative -> fire when x decreasing
	- Close tracking
	- Cost terms required for biologically realistic spike trains (otherwise some neurons extremely high rate, others silent)
- ![Pasted image 20210531110815.png](Pasted%20image%2020210531110815.png)
- If dynamics slower than decoder, integration of sensory signals
- If dynamics faster than decoder, tracking of sensory signals
- Tuning Curve
	- Mean spike count for 1s constant stimulus
	- Monotonic ReLU
	- ![Pasted image 20210531112937.png](Pasted%20image%2020210531112937.png)
	- Homogeneous -> implausible
- Choose randomized kernels instead
	- Weight matrix still constrained (rank=1) $\Gamma_i\Gamma_k$
	- ![Pasted image 20210531113235.png](Pasted%20image%2020210531113235.png)
		- ISI distribution as shown:
		- ![Pasted image 20210531113416.png](Pasted%20image%2020210531113416.png)
		- Delay cross-correlation for same-sign kernel neurons:
		- ![Pasted image 20210531113523.png](Pasted%20image%2020210531113523.png)
		- Not very correlated
- Membrane potentials of neurons with similar kernels ($\Gamma_i^T\Gamma_k>0$) highly correlated, though
	- Homogeneous network: 2 neurons selected
	- ![Pasted image 20210531113830.png](Pasted%20image%2020210531113830.png)
- Rare firing despite strong correlation:
	- Periodic firing required to compensate for leak
	- Exact order of firing doesn't matter due to equal contribution
	- "Integration cycle": All neurons reach threshold at approximately the same time
		- Random neuron fires and inhibits rest
		- New integration cycle begins
		- ![Pasted image 20210531114121.png](Pasted%20image%2020210531114121.png)
- With quadratic cost: Neurons that did not fire recently more likely to reach threshold first
- Inhomogeneous networks: different input to each neuron, different time of threshold reaching
	- Spikes still exhibit Poisson statistics
	- Chaotic network -> single spike change can result in all later spikes being reordered

### 2D Arm Controller
- Application of model to 4-dimensional system
	- 2 arm positions, 2 arm velocities
- $\dot{q}=v$
- $\dot{v}=\lambda_fv+c(t)$
- Motion from central position to different equidistant targets
- Push-pull control with strong acceleration and fast deceleration
- ![Pasted image 20210601090935.png](Pasted%20image%2020210601090935.png)
- Instantaneous firing rates modulated by arm position velocity, force
- ![Pasted image 20210601091016.png](Pasted%20image%2020210601091016.png)
- ReLU tuning curves for arm position
- ![Pasted image 20210601091029.png](Pasted%20image%2020210601091029.png)
- Direction tuning curves are bell shaped
- ![Pasted image 20210601091040.png](Pasted%20image%2020210601091040.png)
- Gain modulation effect of position on tuning curve
- Geometric explanation of tuning properties
- ![Pasted image 20210601091114.png](Pasted%20image%2020210601091114.png)
- cf. [[Dynamic Field Theory#Arm Movement]]

### Differentiation and Oscillation with Heterogeneous Networks
- Additional example: leaky differentiator
	- ![Pasted image 20210601091457.png](Pasted%20image%2020210601091457.png)
	- Computes derivative of $c_1(t)$
	- $c_2(t)=0$
- Additional example: Damped harmonic oscillator
	- Tracks position $x_1(t)$ and speed $x_2(t)$ until very close to zero
	- ![Pasted image 20210601091759.png](Pasted%20image%2020210601091759.png)
- Temporal accuracy limited by $\Gamma$, not $\lambda_d$

## Discussion
- Method for embedding any LDS in recurrent LIF network
- No extensive parameter searches

### Relation to Other Approaches
- NEF Model - relies on linear combination of non-linear rate transfer function of LIF neurons
	- Hence based on firing rates
	- Few predictions about spike statistics
- Detailed balance between excitation and inhibition
- Tight correlation at small time scales (within single ISI)
	- ![Pasted image 20210601095337.png](Pasted%20image%2020210601095337.png)
- Has been observed in several cortical levels
- Firing is regular for small networks, becomes irregular for large ones
	- No impact on performance though
- Model cannot be replaced/approximated by equivalent Poisson generators due to exact timing of spikes being important
	- ![Pasted image 20210601095418.png](Pasted%20image%2020210601095418.png)
	- Errors larger than $\Gamma_i/2$ are immediately corrected by spike
	- This scales as $1/N$
	- Poisson neurons estimation error scales only as $1/\sqrt{N}$
- Combining spike trains recorded in different trials degrades performance strongly
	- Exact spike times matter, not rates
	- ![Pasted image 20210601095448.png](Pasted%20image%2020210601095448.png)
- Finite connectivity, no reduction with N
- Stronger connectivity -> correlation between excitation,inhibition but uncorrelated spike trains
- Currents increase with N, much larger than membrane potential
	- Hence, leak term negligible in large networks
	- Large period of information maintenance (100s when time constant is 0.1s)
	- Persistent firing

### Network Limitations
- Greedy optimization doesn't take into account other costs
	- Problems when  neurons have opposing kernels
	- ping-pong effect: excitatory and inhibitory countering each other
	- can be fixed by increasing spike count cost
- Voltage equation is only approximate
	- In practice, size can be increased to reach acceptable  level of performance
	- FOr given size, approx breaks when A is too large/ c,x too small
- Speed of LDS evolution limited, practically
	- Limited due to noise
	- LDS must compensate for decoder filtering, even though it doesn't place a speed constraint
- Requires finely tuned lateral connections
	- Don't know if this exits in biology
	- Sensitive to global perturbations in excitatory-inhibitory balance

### Experimental Predictions
- Exact scaling of decoding error with N needs to be measured
	- Shared noise introduces correlations and results in error saturation
	- ![Pasted image 20210601095531.png](Pasted%20image%2020210601095531.png)
- Global interaction between neurons of similar selectivity by applying GLM
	- Neurons involved in slow integration tasks or working memory tasks should inhibit and excite each other at different delays.
	-	GLM Filters for integrator discussed earlier:
	-	![Pasted image 20210601095639.png](Pasted%20image%2020210601095639.png)
	-	Recovered shape despite only 2.5% of neurons recorded
-	Network is self-correcting and thus resilient to damage
	-	Sudden inactivation effects:
	-	![Pasted image 20210601095801.png](Pasted%20image%2020210601095801.png)
		-	Two different sets inactivated
		-	No performance degradation at all
	- As long as pool of kernels remains sufficient to track x and firing rates do not saturate, inactivation will not affect network