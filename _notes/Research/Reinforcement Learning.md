[[Research]] [[Machine Learning]] 

# Basics
## Markov decision problem (MDP)
- Agent, environment, states, actions, rewards
- Goal: maximize cumulative rewards
- Set of states: $S$
- Set of actions: $A$
- Set of rewards: $R$
- Agent gets reward based on current state and action taken
	- $f(S_t,A_t)=R_{t+1}$
- Sequence of events: $S_0,A_0,R_1,S_1,A_1,R_2...$
- ![Pasted image 20210909185251.png](Pasted%20image%2020210909185251.png)
## Transition Probabilities
- $S$ and $R$ are finite sets
- Probability that system goes to state $s'$ with reward $r$, given that system is currently in state $s$ and action $a$ is performed:
	- $p(s',r|s,a)=Pr(S_t=s',R_t=r|S_{t-1}=s,A_{t-1}=a)$

## Expected Return
- Return at time $t$:
	- $G_t=R_{t+1}+R_{t+2}...R_T$
	- $T$ is the final time-step
	- Only valid for finite tasks (episodic tasks)
- Goal: maximize expected return
- Infinite tasks <-> continuing tasks
	- Need to define new quantity
	- Discounted return
- Discounted return, with discount rate $\gamma$:
	- $G_t=R_{t+1}+\gamma R_{t+2} + \gamma^2 R_{t+3}...$
	- $G_t=r_{t+1}+\gamma G_{t+1}$

## Policy
- Function that maps a given state to probabilities of actions from that state, denoted $\pi$
- $\pi (a|s)$: probability that $A_t=a$ if $S_t=s$
- $\pi$ is a probability distribution over $A(s)$ for every state $s\in S$

## Value Functions
### State Value Function
- Denoted $v_{\pi}(s)$, for value: Expected return for starting from state $s$ and following policy $\pi$ thereafter
	- $v_{\pi}=E_{\pi}[G_t|S_t=s]$
### Action Value Function
- Denoted $q_{\pi}(s,a)$, for quality: Expected return from starting at state $s$ at time $t$, taking action $a$ and following policy $\pi$ thereafter
	- $q_{\pi}=E_{\pi}[G_t|S_t=s,A_t-a]$
- Also called the Q-function

## Optimality
### Optimal Policy
- Policy $\pi$ is better than or the same as $\pi'$ if:
	- $\pi\geq\pi'$ iff $v_\pi(s)\geq v_{\pi'}(s)$   $\forall s\in S$
	- i.e. expected return is better for all states

### Optimal State Value Function
- Denoted $v*(s)=max_\pi[v_\pi(s)]$
- Gives largest expected return achievable by any policy

### Optimal Action-Value Function
- Optimal q-function, denoted $q_*(s,a)=max_\pi [q_\pi(s,a)]$
- Gives largest expected return achievable by any policy for every state-action pair

## Bellman Optimality Equation
- Property of $q_*$:
	- $q_*(s,a)=E[R_{t+1}+\gamma\; max_{a'}[q_*(s',a')]]$
	- Q-value of this pair is the expected reward for $(s,a)$ plus the maximum expected discounted reward that can be achieved for the next (s',a') pair
- Can be used to find $q_*$ iteratively: Value iteration

## Q-Learning
- Find optimal policy by learning optimal q-values for each state-action pair

### Epsilon Greedy Strategy
- $\epsilon$: probability that the agent chooses an exploratory behavior
- Initially set to 1, decremented whenever a reward is obtained

### Updating the Q-values
- Loss: $q_*(s,a)-q(s,a)$
	- $=E[R_{t+1}+\gamma\; max_{a'}[q_*(s',a')]]-E[\sum_0^\infty \gamma^k R_{t+k+1}]$
- Learning rate: $\alpha \in (0,1]$
- $q^{new}(s,a)=[1-\alpha]q(s,a)+[\alpha](R_{t+1}+\gamma\;max_{a'}q(s',a'))$
	- Convex combination of existing q-value and reward obtained + discounted max. possible return based on previous knowledge

## Deep Q-Learning
- Function approximator to approximate the q-function instead of compute it using value iteration
	- Neural network 
	- Deep Q Network (DQN)
- ![Pasted image 20210914121053.png](Pasted%20image%2020210914121053.png)
	- SGD/BP to train towards ideal q values

### Deep Q Network
- Output layer -> actions
- Input layer -> states
- Are convolutional networks usually as inputs are images in a game etc.

### Experience Replay
- Experience: denoted $e_t = (s_t,a_t,r_{t+1},s_{t+1})$
- Store experiences in a replay memory
	- Finite size, last N experiences are stored
- Randomly sample from set of N experiences to train
	- Only providing sequential experiences gives highly correlated inputs -> inefficient learning
	- Used to break correlation between consecutive samples
- $D$ -> replay memory of size N

### Training a DQN with a Replay Memory
- Policy network
	- Calculates actions from states
- Need to do a second pass to estimate max term in the Bellman equation as it depends on next state, action.
	- Loss: $q_*(s,a)-q(s,a)$
		- $=E[R_{t+1}+\gamma\; max_{a'}[q_*(s',a')]]-E[\sum_0^\infty \gamma^k R_{t+k+1}]$

#### Policy Network Algorithm:
- Initialize replay memory capacity.
- Initialize the network with random weights.
-  _For each episode:_
	-  Initialize the starting state.
	-  _For each time step:_
		-  Select an action via exploration or exploitation
		-  Execute selected action in an emulator.
		-  Observe reward and next state.
		-  Store experience in replay memory.
		-  Sample random batch from replay memory.
		-  Preprocess states from batch.
		-  Pass batch of preprocessed states to policy network.
		-  Calculate loss between output Q-values and target Q-values.
			- Requires a second pass to the network for the next state
		- Gradient descent updates weights in the policy network to minimize loss.

- Problem
	- Target q-values also move with the output q-values from the network and is hence unstable
	- Both are calculated using the same network
	- Use a new network (target network)
#### Target Network
- Clone of policy network
- Weights updated only after many steps
- Used to calculate second pass to estimate max term

#### Full Algorithm
- Initialize replay memory capacity.
- Initialize the policy network with random weights.
- Clone the policy network -> target network
-  _For each episode:_
	-  Initialize the starting state.
	-  _For each time step:_
		-  Select an action via exploration or exploitation
		-  Execute selected action in an emulator.
		-  Observe reward and next state.
		-  Store experience in replay memory.
		-  Sample random batch from replay memory.
		-  Preprocess states from batch.
		-  Pass batch of preprocessed states to policy network.
		-  Calculate loss between output Q-values and target Q-values.
			- Requires a pass to the target network for the next state
		- Gradient descent updates weights in the policy network to minimize loss.
	- After x time steps, weights in the target network are updated to the weights in the policy network