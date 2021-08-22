[[Research]] [[Neuromorphic]]

# Surrogate Gradient Learning in Spiking Neural Networks
[[Friedemann Zenke]] [[Emre Neftci]]

## Mapping SNNs to RNNs
- Internal dynamics of neuron (say, LIF) -> implicit recurrence
	- Discretize and unroll the dynamics of an LIF neuron to get a special case of an RNN
- $\frac{dU^l_i}{dt}=-\frac{1}{\tau}((U_i^l-U_{rest})+RI_i^l)+S_i^l(t)(U_{rest}-v)$
- $\frac{dI^l_i}{dt}=-\frac{I^l_i}{\tau}+\sum W^l_{ij}S_j^{l-1}(t)+\sum V^l_{ij}S_j^l(t)$	
	- Feedforward + recurrent connections
- Discretized using a small time-step($U_{rest}=0,R=1,v=1$):
- $U_i[n+1]=\beta U_i[n]+I_i[n]-S_i[n]$
![Pasted image 20210821090524.png](Pasted%20image%2020210821090524.png)

## Training RNNs
### Temporal CAP
- Backward method:
	- Unroll and do backprop through time
	- $O(NT)$
- Forward method:
	- Compute forward gradient of cost function
	- Typically $O(N^3)$, but can be reduced to $O(N)$ in some cases
	- More biologically plausible

## CAP with Spiking Neurons
- Non-differentiability of spiking non-linearity needs to be overcome
- Locality constraints in hardware need to be met
- Most common approaches
	- Purely using local biological rules like STDP
	- Translating rate-based NNs to SNNs
	- Smoothing network model to be differentiable
	- Defining a surrogate gradient as relaxation of real gradients

### Smoothed SNNs
#### Soft nonlinearity models
- Can be applied directly to all spiking neuron models
- Binary spiking nonlinearity replaced by continuous valued gating function
- Result -> RCNN that can be trained using BPTT
#### Probabilistic models
- Stochasticity smooths out the discontinuous binary nonlinearity
- Gradient defined on expectation values
- Log-likelihood of a spike train is a smooth quantity

> Surrogate Derivatives:
> ![Pasted image 20210821092442.png](Pasted%20image%2020210821092442.png)
> Violet: Step, Green: Piecewise linear, Blue: Sigmoid, Yellow: Exponential

#### Rate coded
- Good performance but may be inefficient
- Somewhat similar to probabilistic models as they use rate coding at the output level
#### Single Spike Timing codes
- Outputs as set of firing times
- More information per spike
- Requires all neurons to be active
	- Can't compute spike time for quiescent units
	- Power efficiency constraint

### Surrogate Gradients
- SG -> Continuous relaxation of the spiking nonlinearity
- ![Pasted image 20210821095339.png](Pasted%20image%2020210821095339.png)
	- a -> linearly interpolated between initial and final weight matrices
	- b-> true gradient obtained through finite difference (itself an approximation)
- Can be used with BPTT
- Do not need to specify coding scheme in hidden layers

### Surrogate Derivative for the Spiking Nonlinearity
- Occurrence of spiking nonlinearity replaced by derivative of differentiable function
	- Nonlinear, monotonically increasing-towards-threshold function
- Performance on par with LSTMs
- Success not dependent on details of surrogate used

## Applications
### Feedback Alignment and Random Error BP
- Approximations to gradient BP rule that sidestep nonlocality problem
	- Weights replaced by random weights
- Random error BP -> errors propagated randomly to each layer
- Little loss in performance
- Feedforward weights adjust themselves to align with the random weights
- Problem -> temporal dynamics of neurons and synapses not accounted for in the gradients
- Solution -> SuperSpike

![Pasted image 20210821102112.png](Pasted%20image%2020210821102112.png)
- a -> BP, b-> FA, c-> DFA, d -> Local Errors (fixed, random cost function at each layer)
### SuperSpike
- Three-factor learning rule
- Online rule that does not require backpropagating error information through time
- Uses synaptic eligibility traces to solve temporal CAP
- Minimizes van Rossum distance between output spike trains and target spike trains using kernel $\lambda$:
	- $L=\frac{1}{2}\sum_{n,i}(\lambda*(S_i[n]-S_i^*[n]))^2$
- Propagates error directly from output layer to hidden units
- Need to compensate for layer-specific delays
- Perform gradient descent on $L$:
- Differentiate network dynamics
	- $\frac{\partial S_i[n+1]}{\partial W_{ij}}=\Theta'(U_i[n+1]-v)[\frac{\partial U_i[n+1]}{\partial W_{ij}}]$
	- $\frac{\partial U_i[n+1]}{\partial W_{ij}}=\beta \frac{\partial U_i[n]}{\partial W_{ij}}+\frac{\partial I_i[n]}{\partial W_{ij}}-\frac{\partial S_i[n]}{\partial W_{ij}}$
	- $\frac{\partial I_i[n+1]}{\partial W_{ij}}=\alpha \frac{\partial I_i[n]}{\partial W_{ij}}+S_{ij}[n]$
- Similar to RTRL equations
- $\Theta$ replaced by smooth function $\sigma$
- Last term in 2nd equation dropped (empirically better results)
- Final weight update:
	- $\Delta W_{ij}[n]\propto e_i[n]\lambda*[\sigma(U_i[n]-v)\frac{\partial U_i[n]}{\partial W_{ij}}]$
	- Only dependent on local quantities
- Becomes nonlocal when applied to more than 2 layers
- Sidestepped by propagating errors to all layers directly through random/fixed weights
- Does not scaled for large multilayer networks

### Learning using Local Errors
- Use layer-wise loss functions
- Forces each layer to learn a set of features that can match top-layer target after linear transforms
- Each layer build on previous layer
- SNN model simplified using feedforward structure
- Cost function defined to operate locally

### Learning using Gradients of Spike Times
- Have well-defined derivatives
- Relies on sparsity
- Example: XOR problem in time (early vs. late)
- First-to-spike code
- ![Pasted image 20210821104330.png](Pasted%20image%2020210821104330.png)

## Conclusions
- Theoretical foundations of SGs for SNNs is an open problem
- Temporal coding makes SNNs quite powerful
- SNNs not as popular as ANNs -> primarily due to trainability issues