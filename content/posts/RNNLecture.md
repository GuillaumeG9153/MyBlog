+++
title = "RNN Lecture"
date = ""
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++

# RNN

What does RNN responds to?

Nowadays, with FFNN we can respond to several types of problems, for instance it can handle a simple problem of sentiment determination in a phrase. Example:

![image info](/MyBlog/lecture1.jpg)

It can handle this problem since it only takes fixed sized vectors as inputs, this is why in this case it used a fixed sized window of one word but because of that, it can lead to wrong predictions especially when double negation is used in a sentence.

This is why we need a new architecture for this type of problem. An architecture with variable length inputs and outputs, that preserve sequential information and have a good generalization over sequences.

### Vanilla RNN

The RNN structure is different since it has a recurrence relation at each step, the function depends of the vector input x and the previous cell state h.

![image info](/MyBlog/lecture2.jpg)

![image info](/MyBlog/lecture3.jpg)

Then we can put these cells in cascade.

![image info](/MyBlog/lecture4.jpg)

How it trains?

We want here to minimize the loss L which is the sum of all the RNN cells so we have to minimize each of them. To do so, we update whh, wxh and why in the direction of the gradient thanks to the backpropagation.
The difficulty here is that gradients are calculated from recurrence relation.

![image info](/MyBlog/lecture5.jpg)

Because of this, we multiply over and over by the same factor whh to calculate the gradient, which leads to 2 problems: An explosion of the gradient if factor > 1 and a vanishing gradient if factor < 1.
The solutions to these problems are the gradient clipping if factors > 1 and a new RNN cell architecture if factors < 1.

### LSTM

LSTM is a kind of RNN with a different cell architecture that avoid these gradients problems.

This is its structure:

![image info](/MyBlog/lecture6.jpg)

The four gates filter information, the ft gate is the forget gate, it decides what information we forget or keep, the input gate it decides which values will be written to current cell, the input modulation gate gt decides how much to write to current cell and finally the ouput ot that decides what will be output from the current cell.

![image info](/MyBlog/lecture7.jpg)

![image info](/MyBlog/lecture8.jpg)

Here the recursive term is constrained thanks to the 4 gates, this permit to avoid the vanishing gradient.

### Deep RNN

Deep RNN is used for language modelling: rephrasing, word prediction, generating text sequences, hand-written text generation, translation and so on.
We can also use this with images to predict next pixels for instance or for image captioning.

### Attention

Attention is defined by the ability to choose what to focus on. Actually, RNN has a memory of pasts events, this is called the implicit attention, but that is not enough. To go deeper, we use new mechanisms called explicit attention that reduce computations, better understand what the Neural Network is doing and that simplify sequential processing. This is how it works.

![image info](/MyBlog/lecture9.jpg)
