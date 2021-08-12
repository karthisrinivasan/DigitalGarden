[[Research]] [[Neuromorphic]] [[Neuroscience]]

# Learning Real-World Stimuli in a Neural Network with Spike-Driven Synaptic Dynamics

## Abstract Learning Rule
- Single output neuron receiving current $h$, weighted sum of activities $s_i$ of $N$ input neurons
	- $h=\frac{1}{N}\sum(J_j-g_I)s_j$
	- $J_j$ - plastic binary weights
	- $g_I$ - inhibitory contribution
- If output neuron should be active and $h<\theta$, $J_j=1$ with probability $q_+s_j$
- If output neuron should be inactive and $h>\theta$, $J_j=0$ with probability $q_-s_j$
- In practice, add/subtract a small value $\delta$ from $\theta$ in the two cases for better performance
- Can learn linearly separable model in finite iterations

## Synaptic Model
- Bistable synapses with value $J_+$ or $J_-$
	- generalized from 0 or 1
- Membrane voltage of LIF: $V(t)$
- Internal state of synapse: $X(t)$
	- Threshold $\theta_X$
- Auxiliary variable: Calcium $C(t)$
	- $\frac{dC}{dt}=-\frac{1}{\tau_C}C(t)+J_C\sum\delta(t-t_i)$
- $X=X+a$ if $V(t_{pre})>\theta_V$ and $\theta^l_{up}<C(t_{pre})<\theta^h_{up}$
- $X=X-b$ if $V(t_{pre})<\theta_V$ and $\theta^l_{down}<C(t_{pre})<\theta^h_{down}$
- $\theta$s - thresholds on calcium variables
- In absence of above conditions being satisfied, passive drift of $X(t)$:
	- $\frac{dX}{dt}=\alpha$ if $X>\theta_X$
	- $\frac{dX}{dt}=-\beta$ if $X<\theta_X$
	- Held if reaches boundary value
- ![Pasted image 20210611194902.png](Pasted%20image%2020210611194902.png)

## Single Synapse Behavior
- ![Pasted image 20210611195007.png](Pasted%20image%2020210611195007.png)
- ![Pasted image 20210611195345.png](Pasted%20image%2020210611195345.png)

## Network Performance
- ![Pasted image 20210611195635.png](Pasted%20image%2020210611195635.png)
- ![Pasted image 20210611200151.png](Pasted%20image%2020210611200151.png)
	- Frequency response histogram
	- time increases back to front
	- Solid - LTD, dashed - LTP

## Parameter Variation Effects
- ![Pasted image 20210611201012.png](Pasted%20image%2020210611201012.png)

## Biological Relevance
- Experimental stimulation protocols applied to synapse model
	- Results agree with real synapses
- ![Pasted image 20210611201422.png](Pasted%20image%2020210611201422.png)
	- Phase related pre and post spikes

