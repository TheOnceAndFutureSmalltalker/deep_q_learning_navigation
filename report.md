# Deep Q Learning Navigation

## Purpose

The purpose of this poject was to use he deep reinforcement learning process known as deep Q Learning to train an agent to navigate a simulated environment full of yellow and blue bananas and gather up as many yellow bananas as possible while ignoring blue bananas.

<br />
<br />
<p align="center"><img src="https://github.com/TheOnceAndFutureSmalltalker/deep_q_learning_navigation/blob/master/images/environment.JPG" width="400px" /> </p>
<p align="center"><b>Simulated Environment of Yellow and Blue Bananas </b></p>

## Design and Implementation

Deep Q-Learning is a technique for finding the Q value function for a given agent in a given environment.  It involves using a neural network as a non-linear function approximator for that function.  It employs the Q-Learning technique to update the Q function.  The input to the neural network is the current state of the environment (sometimes several consecutive states can be stacked as a single input).  This could be an image, a vector of state values, or any other numerial representation of the state of the environment.  The output is a vector of estimated rewards where each entry in the vector represents the reward for one of the possible actions to be taken from that state. Once this vector is generated, the next action can be selected by max, stochastically, using epsilon-greedy, etc.  This output can also be used to calcuate TD values and determine error for the system.  The TD, or Temporal Difference, values are estimates of ground truth using the Q Function itself.

In using such a neural network, the sequence of action-state tuples can become highly correlated.  This problem can be rectified by using the *Experience Replay* technique.  This involves saving the experience tuples in a cache and training from a randomly selected sample of this cache instead of training on each successive tuple as it is generated.

Also, since ground truth used to calculate error for the neural network is itself calculated based on values from the neural network, a second neural network which is held static (weights not updated) for a given number of iterations can be used for this purpose.  This technique is called *Fixed Q Targets*.

### Design

I used a simple neural network with 2 fully connected hidden layers and ReLu activation.  Since the input state is a vector of values and not an image, there was no need for convolutional layers.  One drawback here is that, unlike image states which can be stacked together as a single input, there is no temporal information in the state input in this design. The output is a vector of 4 values, each representing the expected reward for one of the four possible actions.

I also employed the *Experience Replay* and *Fixed Q-Targets* techniques mentioned above.  The full algorithm is shown below, taken from Udacity lesson materials.



The environment is provided in a Unity library and required nothing of me.

### Software Stack

The project is written in Python 3.6 on a Jupyter notebook.  It requires PyTorch, NumPy, and Matlab libraries.  The environment is a Unity implementation which has a Python interface.    

### Implementation

My implementation started with what was provided in the Udacity with some modifications.  The four main components of the implementation are the QNetwork class, the model class,   and the training algorithm mentioned above 


The neural network described above was implemented in the QNetwork class found in Jupyter Notebook file       under heading 

This class was based on the implementation from the Udacity Lesson on Deep Q Learning exercise.  This implementation is seen in the class QNetwork on line   .  It is a simple implementation using PyTorch.

The QNetwork depends on the class     which implements the caching mechanism


Training code is implemented in the Jupyter Notebook file      . under the heading 



## Results

I ran he training several times.  I teaked several of the parameters, but kept returning

## Discussion

