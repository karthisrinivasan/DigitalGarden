[[Research]] [[Neuroscience]] [[Neuromorphic]]

# Optic Nerve Signals in a Neuromorphic Chip I: Outer and Inner Retina Models
[[Kwabena Boahen]]


## Outer Retina Model
- Photons on cone -> reduce current to cone terminal -> decrease in neurotransmitter release
- CTs excite horizontal cells (HCs) -> HCs inhibit CT -> spatiotemporal band-pass signal that adapts to light intensity
- ![[Pasted image 20210802115538.png]]
- Block diagram:
	- ![[Pasted image 20210802115649.png]]
- Spatial frequency response
	- ![[Pasted image 20210802115705.png]]
- ![[Pasted image 20210802120122.png]]
	- $l_c<l_h$ -> cone and horizontal space constants
	- $B$ -> attenuation from CO to CT
	- $A$ -> amplification from CT to HC
- Peak spatial frequency:
	- ![[Pasted image 20210802120358.png]]
- CT activity
	- ![[Pasted image 20210802121038.png]]
	- $\tilde{i}_{CO}$ -> frequency component of $i_{CO}$ at $\rho_A$
	- Activity primarily determined by spatial contrast: $\frac{\tilde{i}_{CO}}{\langle i_{CO}\rangle}$
	- Very similar to mammalian retina:
		- ![[Pasted image 20210802122202.png]]
		- $V_m$ -> max. activation
		- $\sigma$$ -> background intensity
- CMOS Circuit:
	- ![[Pasted image 20210802122417.png]]
	- Photocurrents discharge Vc -> increase CT activity -> excite HC netowrk through NMOS+PMOS mirror
	- HC modulates CT excitation -> inhibits CT activity
	- Vc coupled to 6 nearest neighbors
	- Cone signals gate FETs that feed into BC circuit: Vc increase -> bipolar cell (BC) activity increase
- Cone signal rectification
	- ![[Pasted image 20210802123954.png]]
	- Ic (CT activity) compared to Ir
	- Ic' ~ 1/Ic; Ir' ~ 1/Ir
	- ir'-ic' output through ION and IOFF
	- Asymmetric division

## Inner Retina Model
- Low-pass and high-pass temporal filtering
- ![[Pasted image 20210802124407.png]]
	- BCs excite GCs through wide-field amacrine cells (WAs) and narrow-field amacrine cells (NAs)
	- NAs inhibit BCs,WAs and GCs
	- WAs modulate NA inhibition and spread signals laterally
	- NA -> LPF
	- BT -> HPF
	- ![[Pasted image 20210802130242.png]]
- Block diagram and responses:
	- ![[Pasted image 20210802125015.png]]
- WA receives full-wave rectified input from ON and OFF BT and NA
- BT drives sustained GCs
- BT-NA drives GCtransient
- Loop gain wg set by temporal contrast
- GCt -> purely high-pass response

### Adapting to Temporal Frequency
- Input csin(wit) -> output spectra:
	- ![[Pasted image 20210802130956.png]]
- Loop gain
	- ![[Pasted image 20210802131117.png]]
	- ![[Pasted image 20210802131129.png]]
	- ![[Pasted image 20210802131140.png]]

### Adapting to Contrast
- Point where loop gain saturates with temporal frequency increases with increasing contrast
- ![[Pasted image 20210802131620.png]]
- Loop gain rises sublinearly with contrast and saturates when contrast exceeds some threshold

### Circuit Implementation
- ![[Pasted image 20210802131758.png]]
- The inputs to the circuit, Ic' and Ir', represent complementary inputs to the rectifying BC circuit. 
- We make 5 copies at the outpu(only three are shown in the figure). One copy drives the ON-OFF LPF to excite the NA on one side of the circuit while inhibiting NA on the other side. 
- A second copy is used to excite WAs, which modulates NA feedback inhibition on to BT. 
- The remaining three copies feed ON and OFF versions of transient and sustained GCs.