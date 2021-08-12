[[Research]] [[Neuromorphic]]

# A Spike-Based Neuromorphic Architecture of Stereo Vision

[[Giacomo Indiveri]]

## Event-Based Sensing
- 2 DAVIS sensors - stereo
	- eye-like separation
- Input: frames from these two DVS sensors
## FPGA Interface
![Pasted image 20210623150750.png](Pasted%20image%2020210623150750.png)

##  Processor
- [[DYNAP-SE]]

## SNN Model
- ![Pasted image 20210623150830.png](Pasted%20image%2020210623150830.png)
-  Coincidence and disparity neurons
	-  cyclopean position (x=xR+xL), vertical position (y), disparity (xR-xL)
	-  Location in 3D space
-  Disparity neurons required since 2 targets will cause 4 activity regions in coincidence neurons (see figure)
	-  2 are true targets (TT), 2 are false targets (FT)
-  Disparity population
	-  Recurrent inhibition
	-  FF inhibition from coincidence neurons tuned to same cyclopean position
	-  FF excitation from coincidence neurons tuned to same disparity
	-  Balance between these enables location prediction
- ![Pasted image 20210623151729.png](Pasted%20image%2020210623151729.png)
	- Sample task
	- Bar scanning across field
- ![Pasted image 20210623152022.png](Pasted%20image%2020210623152022.png)
- Output: Location of targets