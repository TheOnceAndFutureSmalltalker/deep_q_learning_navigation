# Deep Q Learning Navigation

## Purpose

The purpose of this poject was to use he deep reinforcement learning process known as deep Q Learning to train an agent to navigate a simulated environment full of yellow and blue bananas and gather up as many yellow bananas as possible while ignoring blue bananas.

## Design and Implementation

### Design

Deep Q Learning is a technique for finding the Q value function for a given agent in  agiven environment.  It involves using a neural network as the Q value function for an agent.  The neural network is trained

fundamentally SARSA

greedy epsilon

Caching technique

2 networks



### Software Stack

The project is written in Python 3.6 on a Jupyter notebook.  It requires PyTorch, NumPy, and Matlab libraries.  The environment is a Unity implementation which has a Python interface.    

### Implementation
I used a simple neural network with 2 fully connected hidden layers and ReLu     .  This class was based on the implementation from the Udacity Lesson on Deep Q Learning exercise.  This implementation is seen in the class QNetwork on line   .  It is a simple implementation using PyTorch.

The QNetwork depends on the class     which implements the caching mechanism

## Results

I ran he training several times.  I teaked several of the parameters, but kept returning

## Discussion

