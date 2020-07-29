# Banana Gobbler

Author: Ashvitha R Shetty

### Project details

Objective: Train an agent to navigate and collect yellow bananas, while avoiding blue bananas

The environment is based on [Unity ML-agents](https://github.com/Unity-Technologies/ml-agents). The Unity Machine Learning Agents Toolkit (ML-Agents) is an open-source Unity plugin that enables games and simulations to serve as environments for training intelligent agents. 

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana. Thus, the goal of your agent is to collect as many yellow bananas as possible while avoiding blue bananas.

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around the agent's forward direction. Given this information, the agent has to learn how to best select actions. Four discrete actions are available, corresponding to:

- 0 - move forward.
- 1 - move backward.
- 2 - turn left.
- 3 - turn right.

The task is episodic, and in order to solve the environment, the agent must get an average score of +13 over 100 consecutive episodes.


### Algorithm and Network Architecture

There are two networks: policy network and target network. They consist of 3 fully connected layers. The hidden layers have 64 neurons each and the output layer has 4 neurons corresponding to each action. ReLU activation is used for all the layers with Adam optimizer.

Algorithm:
- Initialize the replay buffer
- Initialize the policy network with random weights
- Clone the policy network to the target network
- For each episode
    - Initialize the state
    - For each time step
        - Select an action from the policy network according to the epsilon greedy criteria
        - Execute the action
        - Store experience in replay buffer
        - Sample random batches from replay buffer
        - Train the policy network using these batches
        	- Calculate loss between output and target Q values
        	- Minimize the loss using the optimizer
        - After UPDATE_EVERY time steps update weights in the target network using weights in the policy network



### Hyperparameters

- GAMMA: discount rate

- eps: Epsilon is used to select action using epsilon-greedy algorithm. Started with 1 and decayed after each episode
     
- tau: Used for soft update of target network, constant value of 1e-3 was used

- BUFFER_SIZE: Replay buffer  size of 1e5 was used

- BATCH_SIZE: Minibatch size of  64  was used

- UPDATE_EVERY: Episode Interval for network update, the network was updated after every 4 episodes   

### Results

The environment was solved in 438 episodes with an average reward of 13.03 over 100 consecutive episodes. The graph below shows the reward received in each episode.

![](banana_brains_scores.png)

### Future Ideas

1. Use prioritized replay buffer to give importance to rare events during random sampling of events
2. Experiment with network architecture hyperparameters (such as number of hidden layers, neurons in each layer etc. )
