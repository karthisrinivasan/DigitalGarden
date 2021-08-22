[[Research]] [[Neuroscience]] [[Neuromorphic]]

# The van Rossum Distance
[[M.C.W. van Rossum]]

- Method to measure distance between 2 spike trains
	- Filter with exponential kernel and take $l_2$ norm of the difference
- Original spike train:
	- $f_{orig}(t)=\sum\delta(t-t_i)$
- Filtered spike train:
	- $f(t)=\sum u(t-t_i)e^{-(t-t_i)/t_c}$
- Square of the distance, with parameter $t_c$ is defined as:
- $D^2(f,g)_{t_c}=\frac{1}{t_c}\int_0^{\infty}[f(t)-g(t)]^2dt$
- Extreme cases:
	- $t_c=0$
		- $D^2(f,g)=(M+N)/2$
		- M, N are total number of spikes in f and g
		- Counts noncoincident spikes
		- Coincident spikes can be neglected in the limit
	- $t_c=\infty$
		- $D^2(f,g)=(M-N)^2/2$
		- Measures difference in total spike count
- Can also be thought of as weighted integral over the autocorrelation of the difference:
	- $D^2(f,g)=\frac{1}{2}\int_\infty^\infty C_{f-g,f-g}(t)e^{-|t|/t_c}dt$
	- $C$ is autocorrelation of the raw spike trains

## Some Results
- Distance between 2 spike trains differing by a single spike is 1/2
	- $g(t)=f(t)+H(t-t_i)e^{-(t-t_i)/t_c}$
	- $D^2(f,g)=1/2$
	- Independent of $t_c$
- 2 spike trains identical but 1 spike is shifted by some time:
	- $g(t)=f(t)-H(t-t_i)e^{-(t-t_i)/t_c}+H(t-t_i-\delta t)e^{-(t-t_i-\delta t)/t_c}$
	- $D^2(f,g)=1-e^{-|\delta t|/t_c}$
- ![Pasted image 20210821173003.png](Pasted%20image%2020210821173003.png)

## Distance between Uncorrelated Poisson Trains
- Both trains have same rate: $\rho$
- Total duration: $T$
- Average no. of spikes: $\rho T$
	- For small $t_c$, $D^2=\rho T$
- Expectation of $(M-N)^2$ is $2\rho T$ for 2 Poisson processes
	- Hence, $D^2=\rho T$ for large $t_c$
- Using the correlation equation, $D^2=\rho T$, independent of $t_c$
- ![Pasted image 20210821173838.png](Pasted%20image%2020210821173838.png)
	- Mean value for all trials is the same

## Distance between Noise-Driven Spike Trains
- LIF with $\tau=$ 50ms
- Input is Gaussian RV with zero mean and temporal correlation 10ms
- Variance adjusted to give avg. spike frequency of 20Hz
- Gaussian noise added to output spike trains
	- $\sigma_{add}=(0.1)\sigma_{signal}$
- ![Pasted image 20210821174328.png](Pasted%20image%2020210821174328.png)

## Estimating Intrinsic Noise
- Assume neuron has intrinsic noise source
- Add additional noise and extrapolate the distance to estimate intrinsic noise
- ![Pasted image 20210821174714.png](Pasted%20image%2020210821174714.png)
- $\sigma_{total}=\sqrt{\sigma_{add}^2+\sigma_{intrinsic}^2}$