# Solving tennis multi-agent environment using DDPG

## Project details
This project implements the DDPG algorithm to train two agents playing a game of tennis with each other. Each agent attempts to hit the ball over the net and keep the ball in play for as long as possible.

### State space
- Numer of dimension: 8
- Corresponding to the position, velocity of the ball and racket.
- Each agent receives a local observation.
  
### Action space
- Number of dimension: 2
- Corresponding to movement towards or away from net and jumping (continuous number between -1 and 1)
  
### Rewards
- Reward of +0.1 if the agent hits the ball over the net
- Reward of -0.1 if the agent lets the ball hit the ground or hits the ball out of bounds

### Condition for solving environment
The environment is considered solved when the maximum reward over the two agents averages over 0.5 over 100 consecutive episodes

## Getting started

### Instructions for installing dependencies
Below are the necessary python version and python libraries.
  - python: 3.6
  - tensorflow
  - Pillow
  - matplotlib
  - numpy
  - jupyter
  - pytest
  - docopt
  - pyyaml
  - protobuf: 3.5.2
  - grpcio: 1.11.0
  - pandas
  - scipy
  - ipykernel
  - unityagents: 0.4.0
  - torch: 1.10.2

### How to run the code
- Run the Tennis.py to train the model.
- Set the appropriate address to the Unity environment file corresponding to the correct operating system in the code below.
    - env = UnityEnvironment(file_name='Tennis_Windows_x86_64_multiple/Tennis.exe')
- Set load_model_continue_learning = True to load a pre-trained model and continue training.

# Report
## Learning algorithm
- Implemented DDPG algorithm modified to allow multiple agents to add experiences to the experience replay buffer. Because the states are different based on which agent is perceiving it, the actor network and critic network did not need to be implemented separately.
- Found that adding a batch normalization layer to the critic network improves convergence time.
- Found that increasing the soft update rate tau from 1e-3 to 1e-2 improves convergence time.
  
### Hyperparameters
- Replay buffer size = 1e5
- Experience replay minibatch siz = 128 
- Discount factor gamme = 0.99
- Soft update rate tau = 1e-2   
- Actor learning rate = 1e-4    
- Critic learning rate = 1e-3     
- OU noise theta = 0.15
- OU noise sigma = 0.2

### Model architecture
#### Actor network
- Layer 1: Linear fully connected (state_size -> 256) : ReLU activation
- Layer 2: Linear fully connected (256 -> 128) : ReLU activation
  - Layer 2: Linear fully connected (128 -> action_size) : tanh activation

#### Critic network
- Layer 1: Linear fully connected (state_size -> 256) : Leaky ReLU activation
- Batch normalization for output of Layer 1
- Layer 2: Linear fully connected (256+action_size -> 256) : Leaky ReLU activation
- Layer 3: Linear fully connected (256 -> 128) : Leak ReLU activation
- Layer 4: Linear fully connected (128 -> 1) : no activation
  
## Result

### Plot of rewards

## Ideas for future work
- Implement a Critic that outputs a Q-value for both agents' states and actions at the same time
- Implement other policy gradient methods and compare performance
- Change reward structure to create a competitive environment for the two agents. (Obtain reward when opponent agent drops the ball to the ground)
