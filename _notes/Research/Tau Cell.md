[[Research]] [[Analog]] [[Neuromorphic]]

# The Tau Cell: Implementation of Arbitrary Differential Equations
[[Andre van Schaik]]

- [[Subthreshold CMOS Analog Design#Translinear Principle]]
- ![[Pasted image 20210627194124.png]]
	- $i_{i-1}=[\tau_is+1-A_i]i_i+A_ii_{i+1}$
	- $\tau_i=CU_T/I_0$
- ![[Pasted image 20210627191246.png]]
	- $i_{out}i_i=A_iI_0i_{i+1}$
- Cascade of tau cells
	- $T_i=\frac{i_i}{i_{i-1}}=\frac{1}{[\tau_is+1-A_i]i_i+A_iT_{i+1}}$
	- Alternatively, 
	- $T_i=\frac{D_{i+1}}{[\tau_is+1-A_i]D_{i+1}+A_iN_{i+1}}$
		- $N_i=D_{i+1}$
		- $D_i=[\tau_is+1-A_i]D_{i+1}+A_iD_{i+2}$
		- $D_{n+1}=1$
		- $D_n=\tau_ns+1$
	- Hence, $T_i=\frac{D_{i+1}}{D_i}$