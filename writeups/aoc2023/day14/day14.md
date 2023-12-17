# AoC 2023 - Day 14

> `Machine learning` The Little Machine That Wanted to Learn

## Learning Objectives
> - What is machine learning?
> - Basic machine learning structures and algorithms
> - Using neural networks to predict defective toys

## Steps

Task completed using the split-view online. This is a straight walk-through.

### Introduction to machine learning

Day 14
https://tryhackme.com/room/adventofcyber2023


> `Genetic algorithm`: This ML structure aims to mimic the process of natural selection and evolution. By using rounds of offspring and mutations based on the criteria provided, the structure aims to create the "strongest children" through "survival of the fittest".

> `Particle swarm`: This ML structure aims to mimic the process of how birds flock and group together at specific points. By creating a swarm of particles, the structure aims to move all the particles to the optimal answer's grouping point.

> `Neural networks`: This ML structure is by far the most popular and aims to mimic the process of how neurons work in the brain. These neurons receive various inputs that are then transformed before being sent to the next neuron. These neurons can then be "trained" to perform the correct transformations to provide the correct final answer.

> `Supervised learning`: In this learning style, we guide the neural network to the answers we want it to provide. We ask the neural network to give us an answer and then provide it with feedback on how close it was to the correct answer. In this way, we are supervising the neural network as it learns. However, to use this learning style, we need a dataset where we know the correct answers. This is called a labelled dataset, as we have a label for what the correct answer should be, given the input.

> `Unsupervised learning`: In this learning style, we take a bit more of a hands-off approach and let the neural network do its own thing. While this sounds very strange, the main goal is to have the neural network identify "interesting things". Humans are quite good at most classification tasks – for example, simply looking at an image and being able to tell what colour it is. But if someone were to ask you, "Why is it that colour?" you would have a hard time explaining the reason. Humans can see up to three dimensions, whereas neural networks have the ability to work in far greater dimensions to see patterns. Unsupervised learning is often used to allow neural networks to learn interesting features that humans can't comprehend that can be used for classification. A very popular example of this is the restricted Boltzmann machine. Have a look here at the weird features the neural network learned to classify different digits.

> `Input layer`: This is the first layer of nodes in the neural network. These nodes each receive a single data input that is then passed on to the hidden layer. This means that the number of nodes in this layer always matches the network's number of inputs (or data parameters). For example, if our network takes the toy's length, width, and height, there will be three nodes in the input layer.

> `Output layer`: This is the last layer of nodes in the neural network. These nodes send the output from the network once it has been received from the hidden layer. Therefore, the number of nodes in this layer will always be the same as the network's number of outputs. For example, if our network outputs whether or not the toy is defective, we will have one node in the output layer for either defective or not defective (we could also do it with two nodes, but we won't go into that here).

> `Hidden layer`: This is the layer of nodes between the neural network's input and output layers. With a simple neural network, this will only be one layer of nodes. However, for additional learning opportunities, we could add more layers to create a deep neural network. This layer is where the neural network's main action takes place. Each node within the neural network's hidden layer receives multiple inputs from the nodes in the previous layer and will then transmit their answers to multiple nodes in the next layer.

> `Back-Propagation`: When we are training our network, the feed-forward loop is only half of the process. Once we receive the answers from our network, we need to tell it how close it was to the correct answer.

### Code

A guide on how to write the code in python is part of the task. Very informative.

## Question 1

> What is the other term given for Artificial Intelligence or the subset of AI meant to teach computers how humans think or nature works?

machine learning

## Question 2

> What ML structure aims to mimic the process of natural selection and evolution?

genetic algorithm

## Question 3

> What is the name of the learning style that makes use of labelled data to train an ML structure?

supervised learning

## Question 4

> What is the name of the layer between the Input and Output layers of a Neural Network?

back-propagation

## Question 5

> What is the value of the flag you received after achieving more than 90% accuracy on your submitted predictions?

After getting `91.45%` accuracy I uploaded the `predictions.txt` to `http://websiteforpredictions.thm:8000` and got the flag.