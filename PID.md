---
layout: page
title: Implementation and Tuning of a PID Controller
permalink: /PID/
---

I utilized the principles of PID control in order to maneuver a car around a track in simulation. PID control involves setting a controllable feature in order to minimize the error in the outcome. In this situation, the controllable feature is the steering angle of the vehicle, and the outcome is the vehicle’s position on the track. PID control consists of 3 components of error: the error itself (proportional[P]), the change in the error from the previous sample (derivative [D]), and the accumulation of error (integral [I]).

<center><img src="https://live.staticflickr.com/65535/47998063883_fa15c2ae94.jpg"></center>

The image above illustrates the components of error. If the green line represents the target outcome, and the black line represents the actual output, then at the time represented by the last shown black point on the curve: error is shown as the blue line, derivative error is the pink line, and integral error is the yellow space. A PID controller uses 3 constants, one for each component of error, as factors in setting the next control value. Therefore, at this point in time, the controller would set the output (steering angle) as:

<center><img src="https://live.staticflickr.com/65535/47998072737_8c8270f6f7.jpg"></center>

Setting the K values (the constants), is done through a process called tuning. For this project, I used a combination of manual tuning and twiddle, as discussed in the lesson. For manual tuning, I took the baseline steering values of [ -1, 1] to logically decide on starting magnitudes. Since integral error is the largest value, Ki should be the smallest value. The next largest error would likely be proportional error, so Kp is the middle value, and that leaves Kd as the largest value. Using simple factors of 10, I started with Kp=0.01, Ki=0.001, and Kd=0.1. However, in my manner of manual tuning, I started first with a P controller, then made it a PD controller, and finally a PID controller. This allowed me to manually tune each one of the parameters at a time. My self-tuning method was sort of a manual twiddle: my first comparison was multiplying the parameter by 10, and if that was not an improvement, I would divide the original parameter by 10. Then I decreased the magnitude of the change until I found values that were reasonable estimates. The values I found were: 

<center><table>
  <tr>
    <th>Parameter</th>
    <th>Value</th> 
  </tr>
  <tr>
    <td>Kp</td>
    <td>0.05</td> 
  </tr>
  <tr>
    <td>Ki</td>
    <td>0.05</td> 
  </tr>
  <tr>
    <td>Kd</td>
    <td>1.0</td> 
  </tr>
</table></center>

Once I had this starting point, I incorporating twiddle to optimize the parameters further. I started with my aforementioned values, and dp values of {0.01, 0.001, 0.1}, about a factor of 10 below the starting values. The process of twiddle looks like:

* Get the current error
    * Increment the parameter & get the new error:
        * If new error is better:
            * Increment the parameter by a slightly increased increment
        * If new error is not better:
            * Set the parameter to 1 increment below what it was last
            * Get a new error
              * If better error:
                  * Increment the parameter by a slightly increased increment
              * If worse:
                * Go back to the middle value
                * Decrease the increment amount & increment
                

Where all of these steps are looped for each parameter. Twiddle helps to hone in on the optimized value of each parameter. Through utilizing twiddle, resetting my starting values, and running twiddle again, I was able to optimize the K parameters. The final output was:

<center><table>
  <tr>
    <th>Parameter</th>
    <th>Value</th> 
  </tr>
  <tr>
    <td>Kp</td>
    <td>0.0718455</td> 
  </tr>
  <tr>
    <td>Ki</td>
    <td>0.00449649</td> 
  </tr>
  <tr>
    <td>Kd</td>
    <td>1.4344</td> 
  </tr>
</table></center>

and the car was able to drive around the track continuously without leaving the driveable portion of the track.

[GitHub Repo](https://github.com/mmeyer95/PID_Driving)<br>
[Back to Portfolio](https://meredithmeyer.info/)

<br><center>Contact me (below) for more information.</center>
