# Deep Q-Learning Navigation

The code in this project uses a neural network and Deep Q-Learning to estimate the q* function for an agent trying to navigate a world of yellow and blue bananas.  The agent tries to pick up as many yellow bananas as possible while not picking up any blue bananas.  Each yellow banana has a reward of 1 and each blue banana has a reward of -1. The agent can take actions move forward, move backward, turn left, and turn right.  The current environment state is described by a vector of 37 values including things like location, velocity, etc.  The goal is for the agent to maximize his reward.  More specifically, the goal for this project, is for 100 consecutive episodes to have an average reward of over 13.  

<br />
<br />
<p align="center"><img src="https://github.com/TheOnceAndFutureSmalltalker/deep_q_learning_navigation/blob/master/images/environment.JPG" width="400px" /> </p>
<p align="center"><b>Simulated Environment of Yellow and Blue Bananas</b></p>

## Deliverable Files

File | Description
------------ | -------------
checkpoint.pth | Saved weights of Q-Learning neural network.
Navigation.ipynb | Jupyter notebook of runnable code that trains the agent.
report.md | A discussion of the project and the results.


## Dependencies

To run this code, you must have Python 3.6, Jupyter, PyTorch, NumPy, and Matplotlib installed.  You must also have the 

## Instructions

Load the Jupyter Notebook file Navigation.ipynb and execute each cell in succession.  The last cell is the model training and may take several minutes to complete.
