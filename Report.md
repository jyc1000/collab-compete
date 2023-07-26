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
