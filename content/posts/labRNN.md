+++
title = "RNN lab"
date = ""
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
+++

The main goal of this lab is to implement a model that is able to caption an image with a text that describes this image. 

There will be 5 parts for this lab: Dataset description and pre-processing
				  
				  Encoder: pre-trained CNN
				  
				  Decoder: LSTM and Encoder-Decoder model
				  
				  Training
				  
				  Interference

Firstly, we describe our dataset: The one we use is COCO which is famous for object detection and image captioning. We will use here the 2014 version since it has 83k images for training, 41k for validation and 41k for test. In this laboratory we will only use 10k, 2k and 2k for respectively training, validation and testing.

For each set the data is separated in an image and a caption folder. Images are in JPG while captions are stored in a json file, this file specifies to which caption an image is linked.

The first step is to access this dataset:

![image info](/MyBlog/hugo1.jpg)

This is one of the images we displayed:

![image info](/MyBlog/hugo2.jpg)

Then we linked images and captions:

![image info](/MyBlog/hugo3.jpg)

Thanks to this function we can load a dictionary.

Here is an example of captions linked to an image:

![image info](/MyBlog/hugo4.jpg)

Then we create function that permit to retrieve words from these captions.

![image info](/MyBlog/hugo5.jpg)

Then we compute a function that permit to retrieve the unique words.

![image info](/MyBlog/hugo6.jpg)

This permit to get the vocabulary size. So we are able to turn words into vectors.

![image info](/MyBlog/hugo7.jpg)

![image info](/MyBlog/hugo8.jpg)

We also have to do the inverse operation:

![image info](/MyBlog/hugo9.jpg)

# Encoder

In this part we will implement our model that has to be composed of an encoder and a decoder.
The encoder processes the input sequence and extracts features from it. These features will be decoded to produce the output sequence.

Our encoder is a pre-trained CNN on ImageNet.

After we need to encode images:

![image info](/MyBlog/hugo10.jpg)

And then save these images from the encoder and load them from a pickle file.

![image info](/MyBlog/hugo11.jpg)

# Decoder

We will use a LSTM as the decoder, it takes inputs = [images Features, captions] and outputs = next predicted words.

![image info](/MyBlog/hugo12.jpg)







