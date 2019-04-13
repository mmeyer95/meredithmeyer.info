---
layout: page
title: Traffic Sign Classification with a Convolutional Neural Network
permalink: /Signs/
---

The goal of this project was to train a CNN to identify images of German street signs from the LeNet data set. It is important to note that the data is not even distributed among categories. See the chart below: 
<center><img src="https://live.staticflickr.com/7865/46852291614_179d3074db.jpg" width="500" height="304" alt="124"></center>

The CNN I used to train this model is based on the [LeNet-5 CNN](http://yann.lecun.com/exdb/publis/pdf/lecun-bengio-95a.pdf):

<center><img src="https://cdn-images-1.medium.com/max/2400/1*1TI1aGBZ4dybR6__DI9dzA.png"></center>

The model consists of multiple convolutions interspersed with subsamplings (pooling), finished with a few fully-connected layers. I incorporated dropout to minimize over-fitting. The final layers of my model were:
<center><blockquote>Convolutional Layer [5,5,1,6]<br>
Relu Activation<br>
Max Pooling<br>
Convolutional Layer [5, 5, 6, 16]<br>
Relu Activation<br>
Max Pooling<br>
Flattening<br>
Fully Connected Layer (400 to 120)<br>
Relu Activation<br>
40% Dropout<br>
Fully Connected Layer (120 to 84)<br>
Relu Activation<br>
Fully Connected Layer (84 to 43)</blockquote></center>

The last fully connected layer of size 43 maps to the 43 street sign types. After one-hot encoding the logits, each sample image is identified as one of the 43 street signs, based on the maximum probability match.

This model trained with validation accuracy of 93.5%.

[GitHub](https://github.com/mmeyer95/Traffic-Sign-Classifier)<br>
Contact me below for additional information.
