---
title: "Neural Networks from Scratch"
description: "Custom neural network library in Python — backpropagation, multiple activation functions, convolutional layers — no TensorFlow or PyTorch."
status: "In Progress"
emoji: "🧠"
tags: ["Python", "NumPy", "Machine Learning"]
github: "https://github.com/quakeob/neural-networks"
order: 4
---

## The Problem

I was using TensorFlow like everyone else — `model.fit()`, wait, get results. It worked, but I had no idea *why* it worked. What does backpropagation actually compute? Why do certain activation functions perform better? What's really happening inside a convolutional layer?

The only way to truly understand something is to build it from nothing.

## The Approach

Build a complete neural network library using only Python and NumPy. No TensorFlow. No PyTorch. No autograd. Every gradient computed by hand. Every matrix multiplication explicit.

The goal wasn't to compete with production frameworks — it was to understand every single line between input and output.

## What I Built

**Dense layers** with configurable input/output sizes. Forward pass is matrix multiplication plus bias. Backward pass computes gradients with respect to weights, biases, and inputs for chain rule propagation.

**Activation functions:** ReLU, Sigmoid, Tanh, Softmax, Leaky ReLU. Each implemented as a layer with its own forward and backward methods. Writing the Softmax derivative was the moment everything clicked about the Jacobian matrix.

**Convolutional layers.** This is where it got hard. Implementing conv2d from scratch means nested loops over every filter position, every channel, every sample in the batch. The naive implementation is brutally slow — which is exactly why cuDNN exists. But writing it taught me what convolutions *are* in a way that `nn.Conv2d(3, 64, 3)` never could.

**Loss functions:** Cross-entropy, MSE, with proper gradient computation.

**Training loop** with mini-batch SGD, learning rate scheduling, and basic momentum.

## The Aha Moments

**Backpropagation is just the chain rule.** That sounds obvious when you read it, but implementing it layer by layer makes it visceral. Each layer receives a gradient from above and passes a gradient below. That's it. The whole "magic" of neural networks is high school calculus applied recursively.

**Numerical gradient checking** saved me dozens of times. When your analytical gradient disagrees with the numerical approximation, you have a bug. It's a brutally effective debugging tool.

**Matrix shapes are the hard part.** The math isn't conceptually difficult. Getting every transpose, reshape, and broadcast right across batched inputs — that's where the bugs live.

## Stack

- **Language:** Python
- **Math:** NumPy (and nothing else)
- **Visualization:** Matplotlib
- **Validation:** Numerical gradient checking
