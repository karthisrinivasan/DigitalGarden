[[Research]] [[Neuromorphic]]
# A VLSI Analog Computer / Digital Computer Accelerator
- [[Glenn Cowan]] [[Yannis Tsividis]]

- Fast approximate solutions to DEs / co-processor to digital computer
- ![[Pasted image 20210529091716.png]]
### Hybrid Sim Environment
- ~80th order problems
- Combination of analog/digital comps
	- Tight coupling which facilitates calibration
	- Digital programmability
	- Real time sims and obs
	- Fast approx solutions
	- First guess to digital comp to speed up

### VLSI Circuit Design 
- Integrators, VGAs/Multipliers, Fanout blocks, logarithm blocks, exponential blocks, and 
- Programmable blocks:
	- sign, saturation, abs, ramp, min, max, <, >, chopper, track-hold, and sample-hold operations
- ![[Pasted image 20210529092246.png]]

#### Global Design Choices
- Differential mode
- Current-mode
	- Disadvantage - needs fanout block (current mirror)
- Weak inversion circuits for low power consumption

#### Chip Architecture
- 4x4 array of macro-blocks (MBs)
- ![[Pasted image 20210529092343.png]]
- ![[Pasted image 20210529092404.png]]
-  Horizontal/Vertical buses for block i/o
-  Whole chip:
-  ![[Pasted image 20210529095341.png]]
-  Two-level scheme

#### Integrator
- ![[Pasted image 20210529095527.png]]
- Class-A input-output
- $\frac{d}{dt}(i_{outc+}-i_{outc-})=K(i_{in1+}+i_{in2+}-i_{in1-}-i_{in2-})$
	- $K$ - Half of unity gain frequency
- Integrator Core:
	- ![[Pasted image 20210529095752.png]]
- A:B - dual output current mirrors with programmable gains
	- $i_{in1+}=i_{in2+}=-\frac{B}{A}i_{in-}$
	- $i_{in1-}=i_{in2-}=-\frac{B}{A}i_{in+}$
	- B/A = {0.05, 1, 10}
- MV1-5 - generate biases
	- Variable W/L ratio
- B:A - single output current mirrors
	- $i_{out+}=\frac{A}{B}i_{outc+}$
	-  $i_{out-}=\frac{A}{B}i_{outc-}$
	-  A/B = {0.1, 1, 20}
-  Input signal limit = output signal limit
-  $\frac{d}{dt}(i_{outc+}-i_{outc-})=2K(i_{in+}-i_{in-})$
-  UG frequency depends on $I_{TUNE}$
-  "Memory" - stores DAC input word, range settings and other control data

#### Offset Cancellation
- ![[Pasted image 20210529101042.png]]
- Cancellation mode: $mode$ low, $s_{IN}$ high
	- Integrator in UGF
	- $s_{IN}$ lowered and voltage held on $C_{Hold1}$ and $C_{Hold2}$
	- Output current offset also cancelled
	- MD6,7 dummies to alleviate charge injection
	- Charge leakage from caps is CM, and can be corrected by CMFB

#### Current DAC
- Tuning of integrator, VGA, programmable blocks
- MOSFET based R2R ladder
- Deliberately non-monotonic
- ![[Pasted image 20210529101834.png]]
- A) Ideal
- If MSB device draws >> expected current => range of unrealizable outputs (B)
- If MSB device draws << expected current => no unrealizable outputs (C)
- Hence sizes adjusted so that even in presence of mismatch, no unrealizable outputs

#### Variable Gain Amplifier / Multiplier
- Range setting by i/o current mirrors are independent in the differential paths => acts as gain control
- ![[Pasted image 20210529102512.png]]
- $mult$ 
	- LOW 
		- VGA: $i_{o+}-i_{o-}=2\frac{I_T}{1\mu A}(i_{1+}-i_{1-})$
	- HIGH 
		- Multiplier:  $i_{o+}-i_{o-}=2\frac{1}{1\mu A}(i_{1+}-i_{1-})(i_{2+}-i_{2-})$

#### Fanout Block
- ![[Pasted image 20210529102902.png]]
- C - Composite devices
- RANGE LOW - simple current mirror
- CN4 mirrored to CN1-3; CN5 mirrored to CN6-8
- RANGE HIGH - M1,4,8,11,13 on & M3,10 off
	- M2,9  activated - shield inputs from gate capacitance of CN1-3,6-8
- Changing configuration of C devices - variable gain
- 4 quartets of same configuration
	- CN/P 4,5
	- CN/P 1,6
	- CN/P 2,7
	- CN/P 3,8

#### Exponential Circuit
- ![[Pasted image 20210529103712.png]]
- $i_{o+}-i_{o-}=2{I_1}exp(R\frac{i_{in+}-i_{in-}}{n\phi_t})$
- $\phi_t$: thermal voltage
- Single ended exponential needed as it is nonlinear

#### Logarithm Circuit
- ![[Pasted image 20210529103953.png]]
- n-well to source/drain of PMOS acts as diode
- $I_{REF}$ determines zero level
- Only for positive values of $i_{in+}-i_{in-}$
- Saturates before input reaches zero
- $i_{o+}-i_{o-}=G_mn\phi_tlog(\frac{i_{in+}-i_{in-}}{I_{REF}})$

#### Programmable Nonlinear Blocks
- ![[Pasted image 20210529104324.png]]
- I-to-V converter
- ![[Pasted image 20210529104409.png]]

### Measured Results
- 300mW
- ![[Pasted image 20210529104455.png]]
- Worst case block performance:
- ![[Pasted image 20210529104728.png]]
- SNR - 5Hz-1MHz bandwidth
- All numbers normalized to full-scale
- ![[Pasted image 20210529105006.png]]
- ![[Pasted image 20210529105014.png]]
- ![[Pasted image 20210529105020.png]]

### Applications
- Solving ODEs: $\dot{x}=f(x,u,t)$
- Can solve PDEs by converting to ODEs of above form
- Heat Equation Solution (step input):
- ![[Pasted image 20210529105259.png]]

#### Stochastic DEs
- At least one random term whose autocorrelation function is delta
- Tough to solve when system is nonlinear or when random signals are large enough to not be small-signal perturbations
- Example : $\dot{x}=-\nabla f(x)+n(t), f(x)=0.19x^4+0.014x^3-0.25x^2$
- ![[Pasted image 20210529105646.png]]
- Analog computer 24x faster that MATLAB (SunBlade 1000, 4GB RAM)
- ![[Pasted image 20210529105817.png]]

#### True Hybrid Computation
- Analog - moderate accuracy
- Digital - high accuracy but risk of erroneous convergence
- Solving periodic systems:
	- Duffing's equation:
	- $\dot{x}=y$
	- $\dot{y}=x(1-x^2)+Rcos(\omega t)-\gamma y$
- PSIM - program for solving periodic steady state systems
- ~16x speedup when approximate solution fed by analog computer
- ![[Pasted image 20210529110159.png]]

### Conclusion
- Improved analog computers better than this can be made since:
	 1) the reported IC uses simple stack structures, appropriate for lower supply voltages
	 2) design in current mode does not require large voltage swings to achieve adequate dynamic range
	 3) smaller technologies have higher per-unit gate capacitance allowing for smaller integration capacitors
	 4) smaller technologies allow for more compact digital circuitry allowing for more abundant and sophisticated digital calibration schemes
	 5) devices in smaller technologies have higher transition frequencies while still operating in weak inversion, as compared to older technologies
	 6) analog circuits are needed for a variety of other functions in today’s VLSI chips, and thus process development takes performance requirements of such circuits into consideration.