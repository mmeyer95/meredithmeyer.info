---
layout: page
title: WorkOutimal - Smart Exercise Bike
permalink: /Workout/
---
### Skills: Automation, Arduino, Hardware, Sensing, Project Management
##### I developed “WorkOutimal”, a stationary exercise bicycle that is able to guide the rider through an efficient workout.

A play on the words "workout" and "optimal", WorkOutimal was my Capstone project in the M.Eng. program at UC Berkeley. The goal of the project was to create a cardio machine, in our case a bicycle, that is able to guide the user through an efficient workout. Efficient, for our purposes, means maximum calorie expenditure for a given time. This is possible because power output, which is the product of force and velocity, is a nonlinear function for a human.

<center><img src="https://live.staticflickr.com/7904/47596702071_7ed66fbc02.jpg" width="500" height="281" alt="power"></center>

For the project, our team decided to change a previously-existing stationary exercise bike. The bike, pictured stripped-down, is a basic Loctek desk bike which uses a magnet and flywheel to manipulate the resistance to pedaling.

<center><img src="https://static.wixstatic.com/media/4d6d5c_266489fd5d144c33b4eb96328d6cf9b2~mv2_d_5984_3366_s_4_2.jpg/v1/fill/w_920,h_518,al_c,q_85,usm_0.66_1.00_0.01/4d6d5c_266489fd5d144c33b4eb96328d6cf9b2~mv2_d_5984_3366_s_4_2.webp"></center>

<center><img src="https://static.wixstatic.com/media/4d6d5c_471a1cb5dcd4447db211589501da7cda~mv2_d_3024_4032_s_4_2.jpg/v1/fill/w_600,h_800,al_c,q_85,usm_0.66_1.00_0.01/4d6d5c_471a1cb5dcd4447db211589501da7cda~mv2_d_3024_4032_s_4_2.webp"></center>

As part of the hardware duo, my responsibility is to actually create a working product. We are using a 12 volt linear actuator (above) to manipulate the position of the magnet, and thus the resistance on the bike. I will be using an arduino to gauge the speed of pedalling and also to control the linear actuator. So, the first round of the product will be an add-on item to a stationary bicycle.

<center><img src="https://static.wixstatic.com/media/4d6d5c_83c2dd292d944751ba8556effb0363e0~mv2.jpg/v1/fill/w_920,h_710,al_c,q_85,usm_0.66_1.00_0.01/4d6d5c_83c2dd292d944751ba8556effb0363e0~mv2.webp"></center>

The assembly is shown above. In order to measure the pedal velocity, I created a low-fidelity encoder using a single LED and photoresistor. The gaps in the wheel change the reading on the photoresistor, which I then used to calculate the rotations of the flywheel, and then the rotations of the pedals. Both the velocity measurement system and linear actuator are controlled using an Arduino Uno.

<center><img src="https://live.staticflickr.com/7827/46872564974_4f4ff6b3e2.jpg" width="320" height="320" alt="animated"></center>

Again, here is the promotional video for WorkOutimal:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/F1LDj81z75A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[Back to Portfolio](https://meredithmeyer.info/)
<br>
<center>Contact me (below) for more information.</center>
