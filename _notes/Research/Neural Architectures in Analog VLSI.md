[[Research]][[Neuromorphic]]

# Implementing Neural Architectures Using Analog VLSI Circuits
- [[Carver Mead]] [[Misha Mahowald]]

- Neural computation - emergent phenomenon

## System Properties
- Place encodings in biological systems -> AER 
- Carry over across layers -> conformal mapping
- Difference wrt CMOS
	- ~1000 fan-out/in
	- 2+$\epsilon$ dimensions
	- Slower 
-	Need wafer-scale integration

## Circuit Building Blocks
- Voltages -> distribute information
- Currents -> Summing

#### Transistor Model (Subthreshold)
- Behaves like bipolar
- $I=I_{0}e^{KV_g/V_T}e^{-(V_s/V_T)}(1-e^{-(V_{ds}/V_T)}+\frac{V_{ds}}{V_0})$
- $K$ - effectiveness of gate voltage in determining surface potential
- $V_0$ - Early voltage
- Low power consumption
- Drain voltage in subthreshold can be much closer to source voltage
- Exponential inherent

#### Transconductance Amplifier
- ![[Pasted image 20210526220720.png]]
- $I=I_btanh(\frac{K}{2V_T}(V_1-V_2))$
- Wide-range TA used instead
- Incremental gain: $G=I_b\frac{K}{2V_T}$

#### Arithmetic Building Blocks
- WTA <-> Nonspecific inhibition, cf. [[Dynamic Field Theory#Two-Layer DFs]]
- Active resistors in CMOS

#### Photoreceptor
- ![[Pasted image 20210526221903.png]]
- Bipolar - photodetector
- Gain ~100s
- Diode connected PMOS - load (weak inversion region)
- Voltage ~ Log(light intensity)

#### Time-varying Building Blocks
- Follower-integrator (LPF)
	- ![[Pasted image 20210526222337.png]]
- Differentiator: Signal - Integral(signal)
- Neuron
	- current -> spike frequency

## Aggregation
- Follower-aggregator
- ![[Pasted image 20210526222740.png]]
- Contribution by large signals limited due to tanh compression
- Local averaging through resistive-ladder
- ![[Pasted image 20210526223028.png]]
- Continuous network approximation: 
	- $V=V_0e^{-x/L}$
	- $\alpha=1/L=RG$: space constant
	- Multiple inputs cause weighted averaging
	- $V_k=\frac{1}{2G_0}\sum_n\gamma^{n-k}I_n$
	- $G_0$: Effective conductance of semi-infinite network
	- $G_0=\sqrt{\frac{R}{G}}$ for continuous network
- ![[Pasted image 20210526223516.png]]
- Useful for smoothing operation
- 2D version of this is used; weight function more complex

## Silicon Retina
- Generates outputs corresponding to signals in biological retinas in real time
- Pathway 1: Photoreceptor -> triad synapse -> bipolar cell -> ganglion cell
	- Intersects two horizontal pathways: outer and inner plexiform layers
	- Computation performed here
- ![[Pasted image 20210527112632.png]]
- Image becomes independent of absolute light level ; edge enhancement; time derivative emphasis
- ![[Pasted image 20210527112831.png]]
- Horizontal network - resistive network
- Six-neighbor linkage
- Shift in operating point as function of surround illumination
- ![[Pasted image 20210527113509.png]]
	- a) Biological retina
	- b) Silicon retina
- Horizontal layer -> inhibition
- Edge -> transition from below average to above average
- Voltage response of photoreceptors and resistive network along cross section normal to edge
	- ![[Pasted image 20210527114049.png]]
	- Approximation to Laplacian filter

## Sensorimotor Integration
- Conversion from place encoding to frequency encoding for use by motor systems -> saccades etc.

#### Center of Intensity
- Extract information from image
- Engineering oriented approach -> less biologically accurate
- Modified TA, with bias -> phototransistor
- ![[Pasted image 20210527114533.png]]
- $I=I_{photo}tanh(\frac{K}{2V_T}(V_1-V_2))$
	- Variable conductance -> variable gain
- For small input, all amplifiers in linear region
	- Output represents mean
- For large input, output represents median
- 2D Network:
- ![[Pasted image 20210527115324.png]]
- Response to moving stimulus
- ![[Pasted image 20210527115504.png]]
- Can calculate multiple bright spots or display selective attention to single spot

#### Sensorimotor Integration
- [[VLSI Framework for Motor Control]]
- Neuron circuit ; convert servo outputs to pulse train
- Pulsewidth <-> size of correction


