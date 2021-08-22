[[Research]] [[Neuromorphic]]

# Socio-Emotional Robot with Distributed Multi-Platform Neuromorphic Processing
[[Terrence Stewart]] [[Timothy Horiuchi]] [[Andreas Andreou]]

- Simplified amygdala model to determine emotional state from visual input
- Behavioral response
- Processed on SpiNNaker, Loihi and Braindrop
## Existing Social Robots
- Types of social robots
	- Socially evocative -> humans attribute social responsiveness to robot but robot doesn't actually reciprocate (eg. robotic pets)
	- Social interface -> Use cues to convey messages (eg. receptionists)
	- Socially receptive -> Learn from interactions and update internal models but do not interact for social aims
	- Sociable robots -> Have internal goals and motivations and interact for mutual benefit

## Method
- Primate amygdala model
- ![Pasted image 20210821122918.png](Pasted%20image%2020210821122918.png)
	- L -> lateral nucleus
	- B -> basal nucleus
	- AB -> accessory basal nucleus
	- C,M -> central and medial nuclei
	- PFC -> prefrontal cortex, dotes previously determined emotional state
- Processes visual stimuli for emotional relevance
- Value appraisal, provides outputs for an appropriate autonomic response

### Model Overview
- 2,000 neurons and 3 main nuclei
- ![Pasted image 20210821122938.png](Pasted%20image%2020210821122938.png)
- ![Pasted image 20210821122959.png](Pasted%20image%2020210821122959.png)
- Emotional state -> 1 dimensional value
	- 1 for happy, -1 for distress

## Results
- Outputs as partner smiles, frowns, smiles again:
- ![Pasted image 20210821123236.png](Pasted%20image%2020210821123236.png)
- Corresponding spikes and represented values:
- ![Pasted image 20210821123303.png](Pasted%20image%2020210821123303.png)