[[Research]] [[Neuromorphic]]

# Visual explanations from spiking neural networks using inter‑spike intervals
[[Priyadarshini Panda]]

- Conventional method for explaining effect of hidden neurons -> GradCAM
	- Gradient Class Activation Map
	- Done by calculating gradient
	- Doesn't work for SNNs
- New tool -> Spike Activation Map (SAM)
- Short ISI -> more information
	- Calculate Neuronal Contribution Score (NCS)
	- Sum of spike with exponential kernel

## SNN-crafted Grad-CAM
- Computes gradient from output layer to target hidden layer
- Heatmap -> weighted sum of contributions across all channels
- Channel contribution:
	- $\alpha^{c,k}=\frac{1}{N}\sum_i\sum_j\sum_t \frac{\partial y^c}{\partial A^k_{ij,t}}$
	- $A$ -> spike activation of k-th channel and time-step t, (i,j) pixel location
	- Ground truth label -> c
- Weighted sum:
	- $G^c_{ij,t} = max ( 0,\sum_k \alpha^{c,k}_t A^k_{ij,t} )$
	- The SNN-crafted Grad-CAM score
- Suffers from heatmap smoothing effect
	- Caused by approximation of backward gradient

## Spike Activation Map 
- SAM only uses spike activity in forward propagation
- Works without ground truth labels
- Temporal Spike Contribution Score:
	- $T(t,t') = exp (- \gamma |t-t'| )$
- $P^k_{ij}$ -> Set of previous firing times of neuron i k-th channel at location (i,j)
- Compute Neuronal Contribution Score (NCS): $N^k_{ij,t}$:
	- $N^k_{ij,t}=\sum_{t' \in P^k_{ij}}T(t,t')$
	- High if spikes frequently over short interval
- Calculate SAM heatmap $M_{ij,t}$:
	- $M_{ij,t}=\sum_k N^k_{ij,t} S^k_{ij,t}$
	- $S$ -> spike activity of neuron at (i,j) at time step t
- ![Pasted image 20211002093242.png](Pasted%20image%2020211002093242.png)
- Works well when applied to ANNs also

## Results
- Conversion doesn't work as well (less interpretable) than SGD as it doesn't take temporal patterns into account
- SAM more robust to adversarial attacks (small structured perturbations in the input image, parameter $\epsilon$) compared to Grad-CAM in ANNs
	- Temporal processing allowed compensation and correction of noise
	- ![Pasted image 20211002094757.png](Pasted%20image%2020211002094757.png)
- Sensory suppression -> focus on one part of image (when two are concatenated here):
	- ![Pasted image 20211002094826.png](Pasted%20image%2020211002094826.png)