# CarND-Controls-PID Reflection

---

# Effect of P, I, and D Gains:

#### P Controll

The propotional gain of the controller adjust the steering according to the cross track error. However, this correction can lead to overshooting (car going off the tracks) as shown in the video below. The following video has the P value set to `0.09` and all other controller gains were set to `0.0`. 

<p align="center">
	![Propotional controll example](./video_p_example.gif)
</p>

#### D Control

To fix this oscillation we can introduce the derivative gain that sort of predicts the future value of the steering based on the difference between error at two steps. Below is the result of keeping the P-value same as above `0.09` and setting D-value to `3.0`. The oscillation is significantly reduced. 

<p align="center">
	![Propotional controll example](./video_d_example.gif)
</p>

#### I Control

The integral gain can further reduce the error.

## Parameter Tunning

### Kp, Kd, and Ki Tunning

We used manual tunning to adjust the `Kp` , `Kd` and `Ki` gains for the PID-control. Here is the pseudo code for steps followed:

* Increase Kp until the car steering value starts to overshoot a lot.
* Increase Kd to compensate for the overshooting until no further improvement is visible. 
* Use a very small values of Ki to further smooth out the oscillation.  

### Speed

The throttle is set as follows:

```
throttle = 0.1 + ((25.0 - fabs(angle)) / 25.0) * .7 - (fabs(cte) * .05); 

```
The ```angle``` and ```cte``` values are provided by the simulator. We use the angle to determine if we are turnning or driving straight. We set the throttle as a function of how close (or far) the car angle is to being straight. The speed is then discounted by a fixed factor of the steering error - higher the error lower the throttle will be. This help us to recover from errors by reducing the current speed. 

## Result

<p align="center">
	 ![Propotional controll example](./final2.gif)
</p>
