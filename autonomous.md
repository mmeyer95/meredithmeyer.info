---
layout: page
title: Behavioral Cloning in Autonomous Driving
permalink: /autonomous/
---

By collecting data of my own driving habits, creating and training a Convolutional Neural Network (CNN), the simulation was able to learn the proper steering angles to drive on its own. Data took the form of "dash cam" pictures: images of the track from the perspective of what would be the car's dashboard: 

<center><img src="https://live.staticflickr.com/7819/47522991632_6d23a38c0e.jpg" width="320" height="160" alt="center_2016_12_01_13_32_44_569"></center>

However, even with low loss in my neural network training (<3%), the car was not able to stay on the road when driving autonomously. This was likely because when I was controlling the car, there were no sharp turns, and therefore no large steering angles. There was also no way for the network to properly react to seeing the car going off the road, because that was not part of the data it trained on. To supplement the data, I did some "recovery laps": collecting data of the car moving back to the center of the lane after heading off. The training images looked like this:

<center>
<table>
<tr>
    <td><img src="https://live.staticflickr.com/7867/47561987221_b773d2acbb.jpg" width="320" height="160" alt="right_2"></td>
    <td><img src="https://live.staticflickr.com/7818/32619451437_aebdfa8c1f.jpg" width="320" height="160" alt="right_1"></td>
</tr>
<tr>
    <td><img src="https://live.staticflickr.com/7874/32619451517_c9f79b33c5.jpg" width="320" height="160" alt="left_2"></td>
    <td><img src="https://live.staticflickr.com/7810/47561987321_97565d6d12.jpg" width="320" height="160" alt="left_1"></td>
</tr>
</table>
</center>

I also supplemented the data by flipped each image and negating each corresponding steering angle.

I based the structure of my CNN on the [NVIDIA model](https://devblogs.nvidia.com/deep-learning-self-driving-cars/) for a self-driving car:

<center><img src="https://live.staticflickr.com/7899/33685173688_28823799df.jpg" width="448" height="500" alt="CNN"><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script></center>

I also incorporated dropout into my model, to prevent over-fitting. My final loss on the validation data set (0.2 or 20% split from training data) was 1.27%, but most importantly, the simulation was able to drive on its own!

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/k46y8LXDKw8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[GitHub](https://github.com/mmeyer95/BehavioralCloning)<br>
Contact me with questions, below.
