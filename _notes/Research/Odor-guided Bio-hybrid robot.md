[[Research]] [[Neuromorphic]]

# A bio-hybrid odor-guided autonomous palm-sized air vehicle
[[Timothy Horiuchi]]

## Odor Localization
- Many applications (disaster management, leak detection etc.) but limited use due to size, weight and power (SWaP) constraints of small robots
- Plume tracking by animals -> contains near-instant information
	- Turbulent flow allows convection to dominate over diffusion
- Moth antennae outperform SotA chemical sensors

## The Smellicopter: Bio-hybrid system
- Uses antennae from the hawkmoth for a sensor (1.5g, 2.7mW)
	- G-protein mediated chemosensing
- Much faster than MOX (semiconductor metal oxide) sensors
- 30g hovering 4-rotor craft
- Wind fins to passively orient along wind tunnel
	- Reference frame aligned with wind at all times
- Laser ranged distance estimates for obstacle avoidance

## Design
### Structure and Control
- Based on commercially available quadcopter (Crazyflie 2.0)
- ![Pasted image 20210821134436.png](Pasted%20image%2020210821134436.png)

### On-board EAGS and MOX sensors
- Volatile compounds diffuse into the interior of the antenna where they then bind to odor-binding proteins. 
- Those complexes then bind to, and activate, G-protein receptor molecules on the membranes of neurons populating the interior of the antenna. 
- Once activated, G-protein mediated pathways provide a whole cell response that greatly amplifies the influence of a single odorant molecule. 
- That amplified response yields, in turn, an action potential that propagates down the antennal neuron to the brain of the insect.
- EAG represents aggregate electrical activity by voltage drop across length of antenna
- Antennae isolated from moths connected to antennal neural signal amplifier deck (ANSAD) using electrodes
- Lifespan of severed antennae -> many multiples of flight time

### Cast-and-surge Localization
- ![Pasted image 20210821135224.png](Pasted%20image%2020210821135224.png)
- 2D algorithm for detecting and tracking plume
- Move left and right with increasing distances until chemical is detected, then move forward and repeat. Skip to next step if obstacle is detected

## Results
- ![Pasted image 20210821135957.png](Pasted%20image%2020210821135957.png)
- ![Pasted image 20210821135739.png](Pasted%20image%2020210821135739.png)