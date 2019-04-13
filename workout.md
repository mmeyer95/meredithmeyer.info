---
layout: page
title: WorkOutimal - Smart Exercise Bike
permalink: /Workout/
---

A play on the words "workout" and "optimal", WorkOutimal was my Capstone project in the M.Eng. program at UC Berkeley. The goal of the project was to create a cardio machine, in our case a bicycle, that is able to guide the user through an efficient workout. Efficient, for our purposes, means maximum calorie expenditure for a given time. This is possible because power output, which is the product of force and velocity, is a nonlinear function for a human.

For the project, our team decided to change a previously-existing stationary exercise bike. The bike, pictured stripped-down, is a basic Loctek desk bike which uses a magnet and flywheel to manipulate the resistance to pedaling.

As part of the hardware duo, my responsibility is to actually create a working product. We are using a 12 volt linear actuator to manipulate the position of the magnet, and thus the resistance on the bike. I will be using an arduino to gauge the speed of pedalling and also to control the linear actuator. So, the first round of the product will be an add-on item to a stationary bicycle.

The assembly is shown (left). In order to measure the pedal velocity, I created a low-fidelity encoder using a single LED and photoresistor. The gaps in the wheel change the reading on the photoresistor, which I then used to calculate the rotations of the flywheel, and then the rotations of the pedals. Both the velocity measurement system and linear actuator are controlled using an Arduino Uno.

Again, here is the promotional video for WorkOutimal:

<center><iframe width="560" height="315" src="https://www.youtube.com/embed/F1LDj81z75A" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

[Back to Portfolio](https://meredithmeyer.info/)
<br>
<center>Contact me (below) for more information.</center>
