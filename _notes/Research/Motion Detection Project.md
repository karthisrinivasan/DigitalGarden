[[Research]] [[Neuromorphic]] 
### Salient Features
- Ability to detect complex motion that changes direction frequently
	- The network can detect direction of motion accurately even when the stimulus moves in complex non-uniform patterns across the visual field. The neurons respond to changes in direction within the time where the stimulus traverses 3 cells.
- Sensitivity to ranges of stimulus sizes
	- The network can accurately detect stimulus sizes down to a 3x3 square.
- Sparsity
	- The input cell tessellation is not fully-filled, but only has a 68% space-filling ratio, as shown in the tessellation diagram, thereby increasing the size of the visual field that can be covered with the same network size.

## Additions
- Cadence implementation
- Architecture improvement
	- Population of output neurons (stochastic)
	- One output neuron for each velocity range (?)
	- Lateral inhibition 
	- Different time constants in the same network for larger velocity range

## Improvements Based on criticism from ICONS review
- Make explicit improvements paragraph
- Make explicit what the complex task is
- Do complete simulations in SPICE and BRIAN always
- CHECK entire paper yourself
- Mention possible improvements for every shortfall
- Mention time-constants and thresholds for neurons


