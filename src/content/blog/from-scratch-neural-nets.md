---
title: "Building Neural Networks Without TensorFlow"
description: "I built a neural network library from scratch with just NumPy. Here's what I learned that no framework will teach you."
date: 2025-12-20
tags: ["machine-learning", "python", "neural-networks"]
---

# Building Neural Networks Without TensorFlow

Every ML tutorial starts the same way: `pip install tensorflow`. Import some layers. Call `.fit()`. Watch the loss go down. Celebrate.

You just built a neural network! Except you didn't. You assembled one from prefab parts without understanding any of them.

I spent a semester building a neural network library from scratch. Just Python and NumPy. No autograd. No layer abstractions. No `.fit()`. Here's what I learned.

## Why Bother?

Same reason you'd build a CPU in a digital logic class instead of just buying one. The abstractions are leaky, and when they leak — when your model isn't converging and you don't know why — you need to understand what's actually happening.

Also, honestly? It's satisfying. There's a moment when you implement backpropagation by hand, train a network on MNIST, and watch it go from 10% accuracy (random guessing) to 95%+ using nothing but matrix math. That moment is worth the pain.

## Backpropagation, Simply

Everyone overcomplicates backpropagation. Here's what it actually is:

1. You run data forward through the network (forward pass)
2. You compare the output to what you wanted (loss)
3. You figure out how much each weight contributed to the error (backward pass)
4. You nudge each weight in the direction that reduces the error (update)

Step 3 is the "back propagation" part. It's just the chain rule from calculus, applied repeatedly. If you can differentiate `f(g(x))`, you can understand backprop.

The implementation is where it gets spicy. You need to:

- Cache activations from the forward pass (you'll need them for gradients)
- Compute local gradients at each layer
- Multiply them through using the chain rule
- Handle matrix dimensions carefully (this is where 80% of bugs come from)

My first implementation had a dimension mismatch bug that took three days to find. It was a transposed matrix. One `.T`. Three days.

## The Aha Moments

**Aha #1: Activation functions are everything.** Without non-linear activations, a 100-layer network is mathematically equivalent to a single layer. ReLU isn't just a good default — it's what makes deep networks *deep*.

**Aha #2: Learning rate is the most important hyperparameter.** Too high and your loss explodes to infinity. Too low and nothing happens. There's a sweet spot, and finding it is an art. When you implement SGD by hand, you *feel* this in your bones.

**Aha #3: Batch normalization is magic.** I implemented it from the paper. It shouldn't work as well as it does. The fact that normalizing intermediate activations makes everything train better and faster is one of those things that's empirically true but slightly mysterious.

**Aha #4: Gradients vanish and explode.** Train a deep network with sigmoid activations and watch the gradients in the first few layers shrink to zero. This isn't abstract — you can literally print them and watch them disappear. Then switch to ReLU and watch them flow. Now you *understand* the vanishing gradient problem instead of just knowing the phrase.

## What Frameworks Hide From You

When you use PyTorch or TensorFlow:

- **Autograd** handles all the derivative computation. You never think about chain rule.
- **Layer abstractions** hide the weight initialization, the bias terms, the activation application.
- **Optimizers** wrap the update step. Adam isn't just "better SGD" — it's maintaining running averages of gradients and squared gradients. That's complex.
- **GPU acceleration** means you never think about memory layout or CUDA kernels.

These are great abstractions! You should use them for real work. But if you've never looked underneath them, you're building on a foundation you don't understand.

## The Practical Stuff

My library supports:

- Dense (fully connected) layers
- Multiple activation functions (ReLU, sigmoid, tanh, softmax)
- SGD and Adam optimizers
- Cross-entropy and MSE loss
- Basic convolutional layers (these were painful)
- Batch normalization

It trains on MNIST in about a minute on CPU. TensorFlow would do it in seconds on a GPU. That's fine — the point was never performance.

## Should You Do This?

If you're serious about ML: yes. At least once. Build a simple feedforward network, train it on MNIST, implement backprop by hand. You'll come out the other side with an intuition that no amount of tutorial-following can give you.

If you just need to train a model for a project: use PyTorch. Life is short.

But know this — when your model does something weird and you can't figure out why, the person who built one from scratch is going to debug it faster than the person who only knows the API. Every time.
