[[Research]] [[Neuromorphic]]

# Event-Driven Random Back-Propagation: Enabling Neuromorphic Deep Learning Machines
[[Emre Neftci]]

- Inspired by conventional gradient descent and three-factor plasticity rules in biological systems
- Weight update:
	- $\Delta w_{ij}(t) = y_j(t)\phi'(\sum_jw_{ij}(t)y_j(t))T_i(t)$
	- $y_j$ -> presynaptic activity
	- $\phi(.)$ -> activation function  of neuron
	- $T_i(t)=\sum_ke_k(t)g_{ik}$ -> computed as direct random linear combo of errors
	- $e_k$ -> error of output neuron k
	- $g_{ik}$ -> fixed random feedbackw eights to hidden layer neuron i
- eRBP dynamics
	- $\Delta w_{ij}(t)=T_i(t)\Theta(I_i(t))S_j^{pre}(t)$
	- $S$ -> spike train of presynaptic neuron j
	- $\Theta$ -> derivative of activation function evaluated at total input $I_i$
- Boxcar instead of exact $\Theta$ function also works
	- Works coz LIF with refractory period can be approximated as ReLU with threshold
> function eRBP 
	> for k ∈ {presynaptic spike indices $S_{pre}$} do 
	> if $b_{min} < I_i < b_{max}$ then $w_{ik}$ ← $w_{ik} + T_i$,
	> end if 
	> end for 
	> end function

- Weight update performed only when presynaptic neuron fires
- Realization of eRBP requires auxiliary learning variable
	- Substantiated by dendritic compartment