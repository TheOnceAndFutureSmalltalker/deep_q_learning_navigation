# Deep Q Learning Navigation

## Purpose

The purpose of this poject was to use the deep reinforcement learning process known as Deep Q-Learning to train an agent to navigate a simulated environment full of yellow and blue bananas and gather up as many yellow bananas as possible while ignoring blue bananas.

<br />
<br />
<p align="center"><img src="https://github.com/TheOnceAndFutureSmalltalker/deep_q_learning_navigation/blob/master/images/environment.JPG" width="400px" /> </p>
<p align="center"><b>Simulated Environment of Yellow and Blue Bananas </b></p>

## Design and Implementation

Deep Q-Learning is a technique for estimating the q* function for a given agent in a given environment.  It involves using a neural network as a non-linear function approximator for that function.  It employs the Q-Learning technique to update the q function.  The input to the neural network is the current state of the environment (sometimes several consecutive states can be stacked as a single input).  This could be an image, a vector of state values, or any other numerical representation of the state of the environment.  The output is a vector of estimated rewards where each entry in the vector represents the reward for one of the possible actions to be taken from that state. Once this vector is generated, the next action can then be selected by max function, stochastically, using epsilon-greedy policy, etc.  This output can also be used to calculate TD values to determine error for the system.  The TD, or Temporal Difference, values are surrogates of ground truth calculated using the q* function itself.

In using such a neural network, the sequence of action-state tuples can become highly correlated.  This problem can be mitigated by using the *Experience Replay* technique.  This involves saving the experience tuples in a cache and training from a randomly selected sample of this cache instead of training on each successive tuple as it is generated.

Also, since ground truth TD values used to calculate error for the neural network is itself calculated based on values from the neural network, a second neural network which is held static (weights not updated) for a given number of iterations can be used for this purpose.  This technique is called *Fixed Q Targets*.

### Design

I used a simple neural network with 2 fully connected hidden layers, each with 64 neurons, and ReLu activation.  Since the input state is a vector of values and not an image, there was no need for convolutional layers.  One drawback here is that, unlike image states which can be stacked together as a single input, there is no temporal information in the state input in this design. The output is a vector of 4 values, each representing the expected reward for one of the four possible actions.

I also employed the *Experience Replay* and *Fixed Q-Targets* techniques mentioned above.  The full algorithm is shown below, taken from Udacity lesson materials.

<br />
<br />
<p align="center"><img src="https://github.com/TheOnceAndFutureSmalltalker/deep_q_learning_navigation/blob/master/images/algorithm.JPG"  /> </p>
<p align="center"><b>Deep Q-Learning Algorithm </b></p>

The environment is provided in a Unity library and required no implementation on my part.

### Software Stack

The project is written in Python 3.6 on a Jupyter notebook.  It requires PyTorch, NumPy, and Matlab libraries.  The environment is a Unity implementation which has a Python interface.    

### Implementation

My implementation started with what was provided in the Udacity Lesson on Deep Q-Learning with some modifications.  The four main components of the implementation are the QNetwork class, the Agent class, the ReplayBuffer class, and the training algorithm mentioned above.

The QNetwork class is implemented in the Navigation.ipynb file Section 6.  It defines the network architecture and initializes two copies of the neural network described above.  The two copies of the network are for implementing the Fixed Q Targets technique mentioned above.  QNetwork class also conducts forward propagation which is, basically, the q* functionality.  The neural network is implemented using PyTorch. 

The Agent class is implemented in the Navigation.ipynb Section 7.  It depends on the QNetwork class and the ReplayBuffer class.  Its main responsibilities are to determine an action based on a current state, and to take a given action from a given state.  It is also resposible for maintaining the ReplayBuffer and conducting back propagation on the neural network.

The ReplayBuffer class is also implemented in Section 7 of Navigation.ipynb.  It is responsible for maintaining experienced tuples and provided an sample of what is currently in its cached for purposes of training the model.

Finally, the training algorithm is implemented in Section 8 of Navigation.ipynb.  

## Results

I ran the training several times.  I tweaked several of the parameters, but kept returning to the original values as the most productive.  The last qualifying training session is shown at the bottom of the notebook file Navigation.ipynb Section 8.  In this run I was able to satisfy the rubric of 100 episodes averaging a reward of 13 or more.  At the 600th episode, I had a running average over the previous 100 episodes of 14.3.  A plot of these training results in rewards per episode is shown below.  The final weights for the neural network are found in the file checkpoint.pth.

<br />
<br />
<p align="center"><img src="https://github.com/TheOnceAndFutureSmalltalker/deep_q_learning_navigation/blob/master/images/scores.JPG"  /> </p>
<p align="center"><b>Rewards vs Episodes While Training </b></p>

## Discussion

There are several modificatons I could make to the design and implementation above to possibly improve performance and maybe training time (always an issue with nerual networks!).

First, I would like to continue training until the score stabilizes at some maximum value just to see how well I can get the agent to perform.  The main reason I did not do this is time (and money).  

Next, I would like to increase the size of the network to see if that has any effect one things.  This would be increasing both the number of layers and size of the layers.  Again, this is very time consuming.

Finally, there are some additional techniques for Deep Q-Learning I would like to explore.  Primarily, I would like to explore Prioritized Experience Replay.  Instead of sampling from replay buffer at random for training neural network, the tuples in the replay buffer are prioritized by the TD error associated with them.  This makes sure experiences with the most error are revisited to improve the model.  This is very similar to boosting.

