# MITACS Globalink Summer Research Internship
- [[Research]] [[Neuromorphic]]
- [[Glenn Cowan]]
- https://concordia-ca.zoom.us/j/5938434397

## Week 1
- To Do:
	- [x] Ask about TSMC 65nm
	- [x] Finish Reading List
		- [x] MASc Thesis
		- [x] Izhikevich - model
		- [x] Clawson - insect robot
		- [x] Shamsi - low power LIF
		- [x] Tamura - Izhikevich MOS ckt
		- [x] Moradi - DYNAPs
		- [x] Bauer - ECG Anomaly Detection
		- [x] Furber - SpiNNaker
		- [x] Akopyan - TrueNorth
		- [x] Davies - Loihi
	- [ ] Presentation on memristors
		- [ ] Gap dynamics - insulator has trap states, applied voltage generates a directional bias, tunneling happens
		- [ ] Temporal variation of gap - effect of temperature and electric field
		- [ ] How fast state change happens, based on voltage etc. 
	- [x] Read about floating gate memories
- Next meeting:
	- June 9, Wednesday, 9AM Montreal time

## Week 2
- To Do
	- [x] Implement Izhikevich model, characterize regions of operation
		- [x] Use DPIs in the circuit?
		- [x] Alternate implementations
		- [x] Power supply 1.8V / 3.3V
	- [ ] Implement AdExp I&F model (?)
- Next meeting:
	- June 16, Wednesday, 9AM Montreal time
- Working Values (Vc,Vd); td=2n
	- 0.13,0.6 (RS)
	- 0.22, 0.21 (FS)
	- 0.22, {0.55,0.6} (CH)

## Week 3
- To Do
	- [x] Mismatch Simulations
	- [x] Transient Noise
- Next Meeting
	- Monday, June 21

## Week 4+5
- To Do
	- [x] Transient Noise ('crossing' function to determine exact frequency)
	- [x] Reduce device size (0.75x)
		- [x] same behavior? 
			- [x] CH -> 5.5u, (0.25-0.27,0.5-0.6)
			- [x] RS -> 5.5u, (0-0.2,0-0.6)
			- [x] FS -> 5.5u, (0.25-0.3,0-0.5)
			- [x] IB -> 5.5u, (0.27-0.3,0.5-0.6)
		- [x] corners?
		- [ ] mismatch
	- [x] Current input variation
	- [x] Energy per spike computation
		- [x] RS: 19.4uW, ~1.5pJ/spike
		- [x] FS: 49.5uW, ~1.1pJ/spike
		- [x] CH: 38uW, ~1.8pJ/spike
- Next Meeting
	- Tuesday, June 22
	- Week after, no meeting
- [x] FitzHugh Nagumo model
- AdEx behaviors

## Week 6
- [x] Variability
- [ ] Schematic with functional problems
- [x] Slowed circuit
- [ ] Don't change capacitor sizes

## Week 7
- [ ] Why other circuit can't be slowed
- [x] Other behavior
- [x] Mismatch
- [x] Energy
- [ ] Comparison with other implementations
- July 21, 6:30 