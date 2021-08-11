[[Research]] [[Neuroscience]] [[Neuromorphic]] [[MITACS Project]]

# Real-time Ultra-low Power ECG Anomaly Detection using an Event-driven Neuromorphic Processor

[[Felix Bauer]] [[Giacomo Indiveri]]


- Proposed System:
- ![[Pasted image 20210602231632.png]]
- Continuous real-time evaluation
- No segmentation of signal / synchronization to heartbeats
- Analog signal -> Lebesgue sampling -> event/spike trains -> spiking RNN (LIF) -> Linear readout layer to detect anomalous patterns
- Implemented on [[DYNAP-SE]]
- First full-system description of ECG anomaly detector based on a neuromorphic processor

 ## Methods
 ### [[DYNAP-SE]] System
 - Used for spiking RNN implementation

### ECG Data Set, Spike Conversion
-  Labels: Normal / Exhibiting 1 of 18 anomalous conditions
-  0.1-100Hz BPF, 360Hz sampling
-  ![[Pasted image 20210603122651.png]]
-  Conversion to events through a DSM

### sRNN Architecture
- Reservoir computing paradigm
- 3 populations:
	- ff input expansion layer (128)
		- 1-64 excitatory connections (random)
	- recurrent excitatory layer (512)
		- 16 incoming connections from ff
		- 32 recurrent connections
		- 16 from inhibitory
	- non-recurrent inhibitory group (128)
		- 64 connections from excitatory
- ![[Pasted image 20210603122927.png]]
- Random connections and hardware mismatch -> high dimensional representation
- Close to edge of chaos -> rich response

### Learning and Readout
- Exponential kernel for spike filtering
- One readout unit per anomaly type: weighted sum of filtered spiking activities
- Least squares for learning readout weights
- Min. $||Xw^i-y^i||$
	- $X$: Filtered spike trains
	- $w$: Input weights for unit $i$
	- $y$: Target at corresponding time points
		- 1 whenever anomaly is present, 0 otherwise
- Readout unit thresholds:
	- Chosen to minimize false positives and false negatives

## Results
### Performance
- Classification of anomaly type not required; only detection
	- Binary output
- 2.4% false negative rate
- ![[Pasted image 20210603123941.png]]
- Low sensitivity in PVC: reason unknown

### Power Consumption
- 516uW total for [[DYNAP-SE]] chip
- ~700uW including simulated components

## Discussion
- Anomalous patterns usually occur together
	- Missing one beat is not a problem if others are detected
	- Detection of one counts for whole segment
- SVMs / MLPs for readout layer is feasible

### Feasibility of preprocessing and readout stages
- Raw ECG: ~mV, amplifiers exist
- Readout units not neurons
	- Limited fan-in
	- All presynaptic weights same for given synapse type
- Weight quantization
	- May not suffice to quantize pre-trained high-precision weights
	- Learning algorithms exist for finding low precision weights
