TLDR:   
	- Accelerometer inputs should be in g 
	- to make the effect more pronounced, lower or raise betaPeakAmp but never lower it below 1 or it breaks
	- to change the width of the peak change peakWidth to any value (value is squared, so negative is ok) 
	- peakWidth dictates the length of the section where beta is increased as opposed to decreased
	- The 10dof variant of the algorithm requires the acceleration calculated by the altimiter in g or an equivalent system
	- TO ADD lateral acceleration
V 1.0
The change to the original algorithm is changing beta based on accelerometer readings pre-normalization. 
It works by amplifying beta, which prioritizes accelerometer and magnetometer readings when raised.
It uses an inverted quadratic function and two 1/x curves joined together to ensure a very large peak at the desired point (acceleration vector magnitude of one g) and lower values the further out it strays.
Lateral and upward forces of any magnitude work perfectly with this approach, but just like the original, non-dynamic beta version, downward forces with magnitudes over 1 g mess with the orientation. 
In most such cases where gravity is canceled out, it performs better due to the lowered beta when not near the peak, but when inside the peaks regime, it will yield worse results.
A magnetometer helps negate this.

v 1.1
To solve the problem stated above, acceleration about the vertical (along the gravity vector) axis 
from a secondary measurement system (an altimiter is what i designed it for) 
helps activley move the peak due to knowing the true magnitude of the vertical axis acceleration vector
separating lateral forces from vertical ones

PROBLEMS: External vertical forces exceeding 1g that cancel gravity out completley or go even further are currently not coeded in for