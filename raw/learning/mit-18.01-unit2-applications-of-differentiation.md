# MIT 18.01 Single Variable Calculus — Unit 2: Applications of Differentiation

> Source: MIT OpenCourseWare, http://ocw.mit.edu
> Collected: 2026-05-29
> Published: Fall 2006

MIT OpenCourseWare
http://ocw.mit.edu
18.01 Single Variable Calculus
Fall 2006
For information about citing these materials or our Terms of Use, visit: http://ocw.mit.edu/terms.

Lecture 9 18.01 Fall 2006
Lecture 9: Linear and Quadratic Approximations
Unit 2: Applications of Differentiation
Today, we’ll be using differentiation to make approximations.
Linear Approximation
y y = b+a(x-x)
0
b = f(x ) ;a = f’(x )
0 0
y=f(x)
(x ,f(x ))
0 0
x
Figure 1: Tangent as a linear approximation to a curve
The tangent line approximates f(x). It gives a good approximation near the tangent point x .
0
As you move away from x , however, the approximation grows less accurate.
0
f(x) ≈ f(x )+ f�(x )(x − x )
0 0 0
Example 1. f(x) = ln x, x = 1 (basepoint)
0
�
f(1) = ln1=0; f�(1) = 1 � � =1
x �
x=1
ln x ≈ f(1) + f�(1)(x − 1) = 0 + 1 · (x − 1) = x − 1
Change the basepoint:
x = 1 + u =⇒ u = x − 1
ln(1 + u) ≈ u
Basepoint u = x − 1 = 0.
0 0
1

Lecture 9 18.01 Fall 2006
Basic list of linear approximations
In this list, we always use base point x =0 and assume that |x| << 1.
0
1. sin x ≈ x (if x ≈ 0) (see part a of Fig. 2)
2. cos x ≈ 1 (if x ≈ 0) (see part b of Fig. 2)
3. ex ≈ 1+ x (if x ≈ 0)
4. ln(1 + x) ≈ x (if x ≈ 0)
5. (1+ x)r ≈ 1+ rx (if x ≈ 0)
Proofs
Proof of 1: Take f(x) = sin x, then f�(x) = cos x and f(0) = 0
f�(0) = 1,f(x) ≈ f(0) + f�(0)(x − 0) = 0+1.x
So using basepoint x =0,f(x)= x. (The proofs of 2, 3 are similar. We already proved 4 above.)
0
Proof of 5:
f(x) = (1+ x)r; f(0) = 1
d
f�(0) = (1 + x)r| = r(1 + x)r−1| = r
dx x=0 x=0
f(x) = f(0) + f�(0)x =1+ rx
y = x
y=1
sin(x)
cos(x)
(a) (b)
Figure 2: Linear approximation to (a) sin x (on left) and (b) cos x (on right). To find them, apply f (x) ≈ f (x0)+
f�(x0)(x − x0) (x0 = 0)
e−2x
Example 2. Find the linear approximation of f(x) = √ near x = 0.
1+ x
We could calculate f�(x) and find f�(0). But instead, we will do this by combining basic approxi­
mations algebraically.
e−2x ≈ 1+(−2x) (eu ≈ 1+ u, where u = −2x)
2

Lecture 9 18.01 Fall 2006
√ 1
1+ x = (1+ x)1/2 ≈ 1+ x
2
Put these two approximations together to get
e−2x 1 − 2x 1
√ ≈ ≈ (1 − 2x)(1+ x)−1
1+ x 1+ 1 x 2
2
Moreover (1 + 1 x)−1 ≈ 1 − 1 x (using (1 + u)−1 ≈ 1 − u with u = x/2). Thus 1
2 2
e−2x 1 1 1
√ ≈ (1 − 2x)(1 − x)=1 − 2x − x + 2( )x2
1+ x 2 2 2
Now, we discard that last x2 term, because we’ve already thrown out a number of other x2 (and
higher order) terms in making these approximations. Remember, we’re assuming that | x |<< 1.
This means that x2 is very small, x3 is even smaller, etc. We can ignore these higher-order terms,
because they are very, very small. This yields
e−2x 1 5
√ ≈ 1 − 2x − x =1 − x
1+ x 2 2
5 −5
Because f(x) ≈ 1 − x, we can deduce f(0) = 1 and f�(0) = directly from our linear approxi­
2 2
mation, which is quicker in this case than calculating f�(x).
Example 3. f(x) = (1+2x)10 .
(1 + 2x)10 − 1
On the first exam, you were asked to calculate lim . The quickest way to do this with
x→0 x
the tools of Unit 1 is as follows.
(1+2x)10 − 1 f(x) − f(0)
lim = lim = f�(0) = 20
x→0 x x→0 x
(since f�(x) = 10(1+2x)9 · 2=20 at x = 0)
Now we can do the same problem a different way, namely, using linear approximation.
(1 + 2x)10 ≈ 1 + 10(2x) (Use (1 + u)r ≈ 1+ ru where u =2x and r = 10.)
Hence,
(1 + 2x)10 − 1 1+20x − 1
≈ =20
x x
Example 4: Planet Quirk Let’s say I am on Planet Quirk, and that a satellite is whizzing
overhead with a velocity v. We want to find the time dilation (a concept from special relativity)
that the clock onboard the satellite experiences relative to my wristwatch. We borrow the following
equation from special relativity:
T
T � =
�
1 − v2
c2
1 1 1
1A shortcut to the two-step process √ ≈ ≈ 1 − x is to write
1+ x 1+ x 2
2
1 1
√ = (1+ x)−1/2 ≈ 1 − x
1+ x 2
3

Lecture 9 18.01 Fall 2006
satellite
(with velocity v)
me
Figure 3: Illustration of Example 4: a satellite with velocity v speeding past “me” on planet Quirk.
Here, T � is the time I measure on my wristwatch, and T is the time measured onboard the satellite.
� v2 �−1/2 1 � v2 � � v2 1 �
T � = T 1 − ≈ 1+ (1 + u)4 ≈ 1+ ru, where u = − ,r = −
c2 2 c2 c2 2
v2
If v = 4 km/s, and the speed of light (c) is 3 × 105 km/s, ≈ 10−10 . There’s hardly any difference
c2
between the times measured on the ground and in the satellite. Nevertheless, engineers used this very
approximation (along with several other such approximations) to calibrate the radio transmitters
on GPS satellites. (The satellites transmit at a slightly offset frequency.)
Quadratic Approximations
These are more complicated. They are only used when higher accuracy is needed.
f��(x )
f(x) ≈ f(x )+ f�(x )(x − x )+ 0 (x − x )2 (x ≈ x )
0 0 0 2 0 0
Geometric picture: A quadratic approximation gives a best-fit parabola to a function. For
example, let’s consider f(x) = cos(x) (see Figure 4). If x = 0, then f(0) = cos(0) = 1, and
0
f�(x) = − sin(x) =⇒ f�(0) = − sin(0) = 0
f��(x) = − cos(x) =⇒ f��(0) = − cos(0) = −1
1 1
cos(x) ≈ 1+0 · x − x 2 =1 − x 2
2 2
1
You are probably wondering where that in front of the x2 term comes from. The reason it’s
2
there is so that this approximation is exact for quadratic functions. For instance, consider
f(x)= a + bx + cx 2; f�(x)= b +2cx; f��(x)=2c.
Set the base point x = 0. Then,
0
f(0) = a + b ·0+ c · 02 =⇒ a = f(0)
f�(0) = b +2c ·0= b =⇒ b = f�(0)
f��(0)
f��(0) = 2c =⇒ c =
2
4

Lecture 9 18.01 Fall 2006
y
x
cos(x)
1- x2/2
Figure 4: Quadratic approximation to cos(x).
0.0.1 Basic Quadratic Approximations
:
f��(0)
f(x) ≈ f(0) + f�(0)x + x 2 (x ≈ 0)
2
1. sin x ≈ x (if x ≈ 0)
x 2
2. cos x ≈ 1 − (if x ≈ 0)
2
1
3. ex ≈ 1+ x + x2 (if x ≈ 0)
2
1
4. ln(1 + x) ≈ x − x 2 (if x ≈ 0)
2
r(r − 1)
5. (1+ x)r ≈ 1+ rx + x 2 (if x ≈ 0)
2
Proofs: The proof of these is to evaluate f(0),f�(0),f��(0) in each case. We carry out Case 4
f(x) = ln(1 + x) =⇒ f(0) = ln1 = 0
1
f�(x) = [ln(1 + x)]� = =⇒ f�(0) = 1
1+ x
�
1
��
−1
f��(x) = = =⇒ f��(0) = −1
1+ x (1+ x)2
Let us apply a quadratic approximation to our Planet Quirk example and see where it gives.
� v2 �−1/2 1 v2 � ( −1 )( −1 − 1) � v2 �2 � −v2 1
1 − ≈ 1+ + 2 2 − Case 5 with x = ,r = −
c2 2c2 2 c2 c2 2
5

Lecture 9 18.01 Fall 2006
v2 � v2 �2
Since ≈ 10−10, that last term will be of the order ≈ 10−20 . Not even the best atomic
c2 c2
clocks can measure time with this level of precision. Since the quadratic term is so small, we might
as well ignore it and stick to the linear approximation in this case.
e−2x
Example 5. f(x)= √
1+ x
Let us find the quadratic approximation of this expression. We can rewrite it as f(x)= e−2x(1 + x)−1/2 .
Using the approximation of each factor gives
� 1 �� 1 �(− 1)(− 1 − 1) � �
f(x) ≈ 1 − 2x + (−2x)2 1 − x + 2 2 x 2
2 2 2
1 1 3 5 27
f(x) ≈ 1 − 2x − x +(−2)(− )x2 +2x2 + x 2 =1 − x + x 2
2 2 8 2 8
(Note: we drop the x3 and higher order terms. This is a quadratic approximation, so we don’t care
about anything higher than x2.)
6

Lecture 9 18.01 Fall 2006
Lecture 10: Curve Sketching
Goal: To draw the graph of f using the behavior of f� and f��. We want the graph to be
qualitatively correct, but not necessarily to scale.
Typical Picture: Here, y is the minimum value, and x is the point where that minimum occurs.
0 0
y
0
x = critical point
0
Figure 1: The critical point of a function
Notice that for x < x , f�(x) < 0. In other words, f is decreasing to the left of the critical point.
0
For x>x , f�(x) > 0: f is increasing to the right of the critical point.
0
Another typical picture: Here, y is the critical (maximum) value, and x is the critical point. f
0 0
is decreasing on the right side of the critical point, and increasing to the left of x .
0
y
0
f’(x) < 0
x > x
0
x = critical point
0
Figure 2: A concave-down graph
1

Lecture 9 18.01 Fall 2006
Rubric for curve-sketching
1. (Precalc skill) Plot the discontinuities of f — especially the infinite ones!
2. Find the critical points. These are the points at which f�(x) = 0 (usually where the slope
changes from positive to negative, or vice versa.)
3. (a) Plot the critical points (and critical values), but only if it’s relatively easy to do so.
(b) Decide the sign of f�(x) in between the critical points (if it’s not already obvious).
4. (Precalc skill) Find and plot the zeros of f. These are the values of x for which f(x) = 0.
Only do this if it’s relatively easy.
5. (Precalc skill) Determine the behavior at the endpoints (or at ±∞).
Example 1. y =3x − x3
1. No discontinuities.
2. y� =3 − 3x2 = 3(1 − x2) so, y� =0 at x = ±1.
3. (a) At x = 1, y =3 − 1 = 2.
(b) At x = −1, y = −3+1= −2. Mark these two points on the graph.
√
4. Find the zeros: y =3x − x3 = x(3 − x2) = 0 so the zeros lie at x =0, ± 3.
5. Behavior of the function as x → ±∞.
As x →∞, the x3 term of y dominates, so y → −∞. Likewise, as x → −∞, y →∞.
Putting all of this information together gives us the graph as illustrated in Fig. 3)
(1,2)
-2 (-√3,0) -1 1 2
(√3,0)
(-1,-2)
Figure 3: Sketch of the function y =3x − x3. Note the labeled zeros and critical points
Let us do step 3b (the sign of f�) to double-check for consistency.
y� =3 − 3x 2 = 3(1 − x 2)
y� > 0 when |x| < 1; y� < 0 when |x| > 1. Sure enough, y is increasing between x = −1 and x = 1,
and is decreasing everywhere else.
2

Lecture 10 18.01 Fall 2006
1
Example 2. y = .
x
This example illustrates why it’s important to find a function’s discontinuities before looking at the
properties of its derivative. We calculate
−1
y� = < 0
x2
Warning: The derivative is never positive, so you might think that y is always decreasing, and its
graph looks something like that in Fig. 4.
Figure 4: A monotonically decreasing function
1
But as you probably know, the graph of looks nothing like this! It actually looks like Fig. 5. In
x
1
fact, y = is decreasing except at x = 0, where it jumps from −∞ to +∞. This is why we must
x
watch out for discontinuities.
1
Figure 5: Graph of y = .
x
3

Lecture 10 18.01 Fall 2006
Example 3. y = x3 − 3x2 +3x.
y� =3x2 − 6x +3 = 3(x2 − 2x +1) = 3(x − 1)2
There is a critical point at x = 1. y� > 0 on both sides of x = 1, so y is increasing everywhere. In
this case, the sign of y� doesn’t change at the critical point, but the graph does level out (see Fig. 6.
(1,1)
1
horizontal slope
1
Figure 6: Graph of y = y = x3− 3x2 +3x
ln x
Example 4. y = (Note: this function is only defined for x> 0)
x
What happens as x decreases towards zero? Let x =2−n . Then,
ln2−n
y = =(−n ln2)2n → −∞ asn →∞
2−n
In other words, y decreases to −∞ as x approaches zero.
Next, we want to find the critical points.
� ln x �� x( 1 ) − 1(ln x) 1 − ln x
y� = = x =
x x2 x2
y� =0 =⇒ 1 − ln x =0 =⇒ ln x =1 =⇒ x = e
In other words, the critical point is x = e (from previous page). The critical value is
ln e 1
y(x) | = =
x=e e e
4

Lecture 10 18.01 Fall 2006
Next, find the zeros of this function:
y =0 ⇔ ln x =0
So y = 0 when x = 1.
What happens as x →∞? This time, consider x =2+n .
ln2n n ln2 n(0.7)
y = = ≈
2n 2n 2n
So, y → 0 as n →∞. Putting all of this together gets us the graph in Fig. 7.
(e,1/e)
1/e
1 e
Figure 7: Graph of y = ln x
x
Finally, let’s double-check this picture against the information we get from step 3b:
1 − ln x
y� = > 0 for 0 <x<e
x2
Sure enough, the function is increasing between 0 and the critical point.
5

Lecture 10 18.01 Fall 2006
2nd Derivative Information
When f�� > 0, f� is increasing. When f�� < 0, f� is decreasing. (See Fig. 8 and Fig. 9)
slope < 0 slope > 0
slope = 0
Figure 8: f is convex (concave-up). The slope increases from negative to positive as x increases.
Figure 9: f is concave-down. The slope decreases from positive to negative as x increases.
Therefore, the sign of the second derivative tells us about concavity/convexity of the graph. Thus
the second derivative is good for two purposes.
1. Deciding whether a critical point is a maximum or a minimum. This is known as the second derivative
test.
f�(x ) f��(x ) Critical point is a:
0 0
0 negative maximum
0 positive minimum
2. Concave/convex “decoration.”
6

Lecture 10 18.01 Fall 2006
The points where f�� = 0 are called inflection points. Usually, at these points the graph changes
from concave up to down, or vice versa. Refer to Fig. 10 to see how this looks on Example 1.
Inflection point
(where f” = 0)
Figure 10: Inflection point: y =3x − x3, y�� = −6x = 0, at x = 0.
7

Lecture11 18.01 Fa ll 20 06
Lecture 11: Max/Min Problems
ln x
Example 1. y = (same function as in last lecture)
x
1/e
x =e
0
ln x
Figure 1: Graph of y = .
x
1
• What is the maximum value? Answer: y = .
e
• Where (or at what point) is the maximum achieved? Answer: x = e. (See Fig. 1).)
Beware: Some people will ask “What is the maximum?”. The answer is not e. You will get so used
to finding the critical point x = e, the main calculus step, that you will forget to find the maximum
1 1
value y = . Both the critical point x = e and critical value y = are important. Together, they
e e
1
form the point of the graph (e, ) where it turns around.
e
Example 2. Find the max and the min of the function in Fig. 2
Answer: If you’ve already graphed the function, it’s obvious where the maximum and minimum
values are. The point is to find the maximum and minimum without sketching the whole graph.
Idea: Look for the max and min among the critical points and endpoints.You can see from Fig. 2
that we only need to compare the heights or y-values corresponding to endpoints and critical points.
(Watch out for discontinuities!)
1

Lecture11 18.01 Fa ll 20 06
max
min
Figure 2: Search for max and min among critical points and endpoints
Example 3. Find the open-topped can with the least surface area enclosing a fixed volume, V.
h
r
Figure 3: Open-topped can.
1. Draw the picture.
2. Figure out what variables to use. (In this case, r, h, V and surface area, S.)
3. Figure out what the constraints are in the problem, and express them using a formula. In this
example, the constraint is
V = πr2h = constant
We’re also looking for the surface area. So we need the formula for that, too:
S = πr2 + (2πr)h
Now, in symbols, the problem is to minimize S with V constant.
2

Lecture11 18.01 Fa ll 20 06
4. Use the constraint equation to express everything in terms of r (and the constant V ).
� �
V V
h = ; S = πr2 + (2πr)
2πr πr2
5. Find the critical points (solve dS/dr = 0), as well as the endpoints. S will achieve its max and
min at one of these places.
dS 2V V
�
V
�1/3
=2πr − =0 =⇒ πr3 − V =0 =⇒ r 3 = =⇒ r =
dr r2 π π
We’re not done yet. We’ve still got to evaluate S at the endpoints: r =0 and “r = ∞”.
2V
S = πr2 + , 0 ≤ r < ∞
r
2
As r → 0, the second term, , goes to infinity, so S → ∞. As r → ∞, the first term πr2 goes
r
to infinity, so S → ∞. Since S = +∞ at each end, the minimum is achieved at the critical point
r =(V/π)1/3, not at either endpoint.
s
to ∞
to ∞
r
Figure 4: Graph of S
We’re still not done. We want to find the minimum value of the surface area, S, and the values
of h.
�
V
�1/3
V V V
�
V
�−2/3 �
V
�1/3
r = ; h = = = =
π πr2
π
�V �2/3 π π π
π
V
�
V
�2/3 �
V
�1/3
S = πr2 +2 = π +2V =3π−1/3V 2/3
r π π
Finally, another, often better, way of answering that question is to find the proportions of the
h h (V/π)1/3
can. In other words, what is ? Answer: = = 1.
r r (V/π)1/3
3

Lecture11 18.01 Fa ll 20 06
Example 4. Consider a wire of length 1, cut into two pieces. Bend each piece into a square. We
want to figure out where to cut the wire in order to enclose as much area in the two squares as
possible.
0 x 1
(1/4)x
(1/4)(1-x)
Figure 5: Illustration for Example 5.
The first square will have sides of length x. Its area will be x2 . The second square will have
4 16
sides of length 1−x . Its area will be �1−x �2 . The total area is then
4 4
� x �2 � 1 − x �2
A = +
4 4
2x 2(1− x) x 1 x 1
A� = + (−1) = − + =0 =⇒ 2x − 1=0 =⇒ x =
16 16 8 8 8 2
So, one extreme value of the area is
� 1 �2 � 1 �2 1
A = 2 + 2 =
4 4 32
We’re not done yet, though. We still need to check the endpoints! At x = 0,
�
1 − 0
�2
1
A =02 + =
4 16
At x = 1,
�
1
�2
1
A = +02 =
4 16
4

Lecture11 18.01 Fa ll 20 06
By checking the endpoints in Fig. 6, we see that the minimum area was achieved at x = 1.
2
The maximum area is not achieved in 0 < x < 1, but it is achieved at x = 0 or 1. The maximum
corresponds to using the whole length of wire for one square.
Area
1/16
1/32
x
1/2 1
Figure 6: Graph of the area function.
Moral: Don’t forget endpoints. If you only look at critical points you may find the worst answer,
rather than the best one.
5

Lecture 12 18.01 Fa ll 20 06
Lecture 12: Related Rates
Example 1. Police are 30 feet from the side of the road. Their radar sees your car approaching at
80 feet per second when your car is 50 feet away from the radar gun. The speed limit is 65 miles
per hour (which translates to 95 feet per second). Are you speeding?
First, draw a diagram of the setup (as in Fig. 1):
Police
30
D=50
Car
Road
x
Figure 1: Illustration of example 1: triangle with the police, the car, the road, D and x labelled.
Next, give the variables names. The important thing to figure out is which variables are changing.
dD
At D = 50, x = 40. (We know this because it’s a 3-4-5 right triangle.) In addition, = D� =
dt
−80. D� is negative because the car is moving in the −x direction. Don’t plug in the value for D
yet! D is changing, and it depends on x.
The Pythagorean theorem says
302 + x 2 = D2
Differentiate this equation with respect to time (implicit differentiation:
d � 3 02 + x 2 = D2� =⇒ 2xx� =2DD� =⇒ x� = 2DD�
dt 2x
Now, plug in the instantaneous numerical values:
50 feet
x� = (−80) = −100
40 s
This exceeds the speed limit of 95 feet per second; you are, in fact, speeding.
1

Lecture 12 18.01 Fa ll 20 06
There is another, longer, way of solving this problem. Start with
�
D = 302 + x2 = (302 + x2 )1/2
d 1 dx
D = (302 + x2 )−1/2(2x )
dt 2 dt
Plug in the values:
1 dx
−80= (302 + 402)−1/2(2)(40)
2 dt
and solve to find
dx feet
= −100
dt s
√
(A third strategy is to differentiate x = D2 − 302). It is easiest to differentiate the equation in its
simplest algebraic form 302 + x2 = D2, our first approach.
The general strategy for these types of problems is:
1. Draw a picture. Set up variables and equations.
2. Take derivatives.
3. Plug in the given values. Don’t plug the values in until after taking the derivatives.
Example 2. Consider a conical tank. Its radius at the top is 4 feet, and it’s 10 feet high. It’s being
filled with water at the rate of 2 cubic feet per minute. How fast is the water level rising when it is
5 feet high?
r
h
Figure 2: Illustration of example 2: inverted cone water tank.
From Fig. 2), the volume of the tank is given by
1
V = πr2h
3
2

Lecture 12 18.01 Fa ll 20 06
The key here is to draw the two-dimensional cross-section. We use the letters r and h to represent
the variable radius and height of the water at any level. We can find the relationship between r and
h from Fig. 3) using similar triangles.
4
r
10
h
Figure 3: Relating r and h.
From Fig. 3), we see that
r 4
=
h 10
or, in other words,
2
r = h
5
Plug this expression for r back into V to get
1
�
2
�2
4
V = π h h = πh3
3 5 3(25)
dV 4
= V � = πh2h�
dt 25
dV
Now, plug in the numbers ( = 2, h = 5):
dt
� �
4
2= π(5)2h�
25
1
h� =
2π
Related rates also arise on Problem Set 3 (Fig. 4). There’s a part II margin of error problem
ΔL
involving a satellite, where you’re asked to find .
Δh
3

Lecture 12 18.01 Fa ll 20 06
satellite
h
c
L
Figure 4: Illustration of the satellite problem.
L2 + c2 = h2
2LL� = 2hh�
ΔL L� h
Hence, ≈ =
Δh h� L
There is also a parabolic mirror problem based on similar ideas (Fig. 5).
Δa
Δθ
Figure 5: Illustration of the parabolic mirror problem.
Δa Δθ
Here, you want to find either or . This type of sensitivity of measurement problem
Δθ Δa
matters in every measurement problem, for instance predicting whether asteroids will hit Earth.
4

Lecture 13 18.01 Fall 2006
Lecture 13: Newton’s Method and Other
Applications
Newton’s Method
Newton’s method is a powerful tool for solving equations of the form f(x) = 0.
Example 1. f(x) = x2 − 3. In other words, solve x2 − 3 = 0. We already know that the solution
√
to this is x = 3. Newton’s method, gives a good numerical approximation to the answer. The
method uses tangent lines (see Fig. 1).
y = x2 -3
x=1 x
0 1
(1,-2)
Figure 1: Illustration of Newton’s Method, Example 1.
The goal is to find where the graph crosses the x-axis. We start with a guess of x = 1. Plugging
0
that back into the equation for y, we get y =12 − 3= −2, which isn’t very close to 0.
0
Our next guess is x , where the tangent line to the function at x crosses the x-axis. The equation
1 0
for the tangent line is:
y − y = m(x − x )
0 0
When the tangent line intercepts the x-axis, y = 0, so
−y = m(x − x )
0 1 0
y
− 0 = x − x
m 1 0
y
x = x − 0
1 0 m
Remember: m is the slope of the tangent line to y = f(x) at the point (x ,y ).
0 0
1

Lecture 13 18.01 Fall 2006
In terms of f:
y = f(x )
0 0
m = f�(x )
0
Therefore,
f(x )
x = x − 0
1 0 f�(x )
0
x x
0 2
x
1
Figure 2: Illustration of Newton’s Method, Example 1.
In our example, f(x)= x2 − 3,f�(x)=2x. Thus,
(x2 − 3) 1 3
x = x − 0 = x − x +
1 0 2x 0 2 0 2x
0
1 3
x = x +
1 2 0 2x
0
The main idea is to repeat (iterate) this process:
1 3
x = x +
2 2 1 2x
1
1 3
x = x +
3 2 2 2x
2
√
and so on. The procedure approximates 3 extremely well.
2

Lecture 13, Version 3.0 18.01 Fall 2006
√
x y accuracy: |y − 3|
x 1
0
x 2 3 × 10−1
1
x 7 2 × 10−2
2 4
x 7 + 6 10−4
3 8 7
x 18,817 3 × 10−9
4 10,864
Notice that the number of digits of accuracy doubles with each iteration.
Summary
Newton’s Method is illustrated in Fig. 3 and can be summarized as follows:
f(x )
x = x − k
k+1 k f�(x )
k
y=f(x)
(x , y )
k k
x
k+1
x = kth iterate
k
Figure 3: Illustration of Newton’s Method.
Example 1 considered the particular case of
f(x) = x2 − 3
f(x ) 1 3
x = x − k = ... = x +
k+1 k f�(x ) 2 k 2x
k k
Now, we define
x = lim x (x → x as k →∞)
k k
k→∞
To evaluate x in Example 1, take the limit as k →∞ in the equation
1 3
x = x +
k+1 2 k 2x
k
3

Lecture 13, Version 3.0 18.01 Fall 2006
This yields
1 3 1 3 1 3
x¯= x¯+ =⇒ x − x = =⇒ x = =⇒ x 2 =3
2 2x¯ 2 2x 2 2x
√
which is just what we hoped: x = 3.
Warning 1. Newton’s Method can find an unexpected root.
√ √
Example: if you take x = −1, then x → − 3 instead of + 3. This convergence to an unexpected
0 k
root is illustrated in Fig. 4
y = x2-3
x
0
x
1
tangent to
curve at x = x
0
Figure 4: Newton’s method converging to an unexpected root.
Warning 2. Newton’s Method can fail completely.
This failure is illustrated in Fig. 5. In this case, x = x , x = x , and so forth. It repeats in a
2 0 3 1
cycle, and never converges to a single value.
(x , y )
1 1
x
0
x
1
(x , y )
0 0
Figure 5: Newton’s method converging to an unexpected root.
4

Lecture 13 18.01 Fall 2006
Ring on a String
Consider a ring on a string 1 held fixed at two ends at (0, 0) and (a,b) (see Fig. 6). The ring is
free to slide to any point. Find the position (x,y) of the string.
a-x
(a, b)
(0, 0)
x
√ [(a-x)2 +(b-y2)]
β
α
√ (x2 +y2)
α = β
(x, y)
Figure 6: Illustration of the Ring on a String problem.
Physical Principle The ring settles at the lowest height (lowest potential energy), so the prob­
lem is to minimize y subject to the constraint that (x,y) is on the string.
Constraint The length L of the string is fixed:
� �
x2 + y2 + (x − a)2 +(y − b)2 = L
The function y = y(x) is determined implicitly by the constraint equation above. We traced the
constraint curve (possible positions of the ring) on the blackboard. This curve is an ellipse with foci
at (0, 0) and (a,b), but knowing that the curve is an ellipse does not help us find the lowest point.
Experiments with the hanging ring show that the lowest point is somewhere in the middle. Since
the ends of the constraint curve are higher than the middle, the lowest point is a critical point
(a point where y�(x) = 0). In class we also gave a physical demonstration of this by drawing the
horizontal tangent at the lowest point.
To find the critical point, differentiate the constraint equation implicitly with respect to x,
x + yy� x − a +(y − b)y�
+ =0
� �
x2 + y2 (x − a)2 +(y − b)2
Since y� = 0 a the critical point, the equation can be rewritten as
x a − x
=
� �
x2 + y2 (x − a)2 +(y − b)2
1�c1999 and �c2007 David Jerison
5

Lecture 13 18.01 Fall 2006
From Fig. 6, we see that the last equation can be interpreted geometrically as saying that
sin α = sin β
where α and β are the angles the left and right portions of the string make with the vertical.
Physical and geometric conclusions
The angles α and β are equal. Using vectors to compute the force exerted by gravity on the two
halves of the string, one finds that there is equal tension in the two halves of the string - a physical
equilibrium. (From another point of view, the equal angle property expresses a geometric property
of ellipses: Suppose that the ellipse is a mirror. A ray of light from the focus (0, 0) reflects off the
mirror according to the rule angle of incidence equals angle of reflection, and therefore the ray goes
directly to the other focus at (a,b).)
Formulae for x and y
We did not yet find the location of (x,y). We will now show that
a � b � 1 � � �
x = 1 − √ , y = b − L2 − a2
2 L2 − a2 2
Because α = β,
� �
x = x2 + y2 sin α; a − x = (x − a)2 +(y − b)2 sin α
Adding these two equations,
�� � � a
a = x2 + y2 + (x − a)2 +(y − b)2 sin α = L sin α =⇒ sin α =
L
The equations for the vertical legs of the right triangles are (note that y < 0):
� �
−y = x2 + y2 cos α; b − y = (x − a)2 +(y − b)2 cos β
Adding these two equations, and using α = β,
�� � � 1
b − 2y = x2 + y2 + (x − a)2 +(y − b)2 cos α = L cos α =⇒ y = (b − L cos α)
2
a � √
Use the relation sin α = to write L cos α = L 1 − sin2 α = L2 − a2. Then the formula for y is
L
1 � � �
y = b − L2 − a2
2
Finally, to find the formula for x, use the similar right triangles
x a − x
tan α = = =⇒ x(b − y)=(−y)(a − x) =⇒ (b − 2y)x = −ay
−y b − y
Therefore,
� �
−ay a b
x = = 1 − √
b − 2y 2 L2 − a2
Thus we have formulae for x and y in terms of a, b and L.
I omitted the derivation of the formulae for x and y in lecture because it is long and because we
got all of our physical intuition and understanding out of the problem from the balance condition
that was the immediate consequence of the critical point computation.
Final Remark. In 18.02, you will learn to treat constrained max/min problems in any number
of variables using a method called Lagrange multipliers.
6

Lecture 14 18.01 Fall 2006
Lecture 14: Mean Value Theorem and Inequalities
Mean-Value Theorem
The Mean-Value Theorem (MVT) is the underpinning of calculus. It says:
If f is differentiable on a<x<b, and continuous on a ≤ x ≤ b, then
f(b) − f(a)
= f�(c) (for some c, a<c<b)
b − a
f(b) − f(a)
Here, is the slope of a secant line, while f�(c) is the slope of a tangent line.
b − a
secant line
slope
f’(c)
b
a c
Figure 1: Illustration of the Mean Value Theorem.
Geometric Proof: Take (dotted) lines parallel to the secant line, as in Fig. 1 and shift them up
from below the graph until one of them first touches the graph. Alternatively, one may have to start
with a dotted line above the graph and move it down until it touches.
If the function isn’t differentiable, this approach goes wrong. For instance, it breaks down for
the function f(x)= |x|. The dotted line always touches the graph first at x = 0, no matter what its
slope is, and f�(0) is undefined (see Fig. 2).
1

Lecture 14 18.01 Fall 2006
Figure 2: Graph of y = |x|, with secant line. (MVT goes wrong.)
Interpretation of the Mean Value Theorem
You travel from Boston to Chicago (which we’ll assume is a 1,000 mile trip) in exactly 3 hours. At
1000
some time in between the two cities, you must have been going at exactly mph.
3
f(t) = position, measured as the distance from Boston.
f(3) = 1000, f(0) = 0, a =0, and b=3.
1000 f(b) − f(a)
= = f�(c)
3 3
where f�(c) is your speed at some time, c.
Versions of the Mean Value Theorem
There is a second way of writing the MVT:
f(b) − f(a) = f�(c)(b − a)
f(b) = f(a)+ f�(c)(b − a) (for some c,a < c < b)
There is also a third way of writing the MVT: change the name of b to x.
f(x)= f(a)+ f�(c)(x − a) for some c,a < c < x
The theorem does not say what c is. It depends on f, a, and x.
This version of the MVT should be compared with linear approximation (see Fig. 3).
f(x) ≈ f(a)+ f�(a)(x − a) x near a
2

Lecture 14 18.01 Fall 2006
The tangent line in the linear approximation has a definite slope f�(a). by contrast formula is an
exact formula. It conceals its lack of specificity in the slope f�(c), which could be the slope of f at
any point between a and x.
(x,f(x))
error
(a,f(a))
y=f(a) + f’(a)(x-a)
Figure 3: MVT vs. Linear Approximation.
Uses of the Mean Value Theorem.
Key conclusions: (The conclusions from the MVT are theoretical)
1. If f�(x) > 0, then f is increasing.
2. If f�(x) < 0, then f is decreasing.
3. If f�(x) = 0 all x, then f is constant.
Definition of increasing/decreasing:
Increasing means a<b ⇒f(a) <f(b). Decreasing means a<b =⇒ f(a) <f(b).
Proofs:
Proof of 1:
a < b
f(b) = f(a)+ f�(c)(b − a)
Because f�(c) and (b − a) are both positive,
f(b)= f(a)+ f�(c)(b − a) >f(a)
(The proof of 2 is omitted because it is similar to the proof of 1)
Proof of 3:
f(b)= f(a)+ f�(c)(b − a)= f(a) + 0(b − a)= f(a)
Conclusions 1,2, and 3 seem obvious, but let me persuade you that they are not. Think back to the
definition of the derivative. It involves infinitesimals. It’s not a sure thing that these infinitesimals
have anything to do with the non-infinitesimal behavior of the function.
3

Lecture 14 18.01 Fall 2006
Inequalities
The fundamental property f� > 0 =⇒ f is increasing can be used to deduce many other inequali­
ties.
Example. ex
1. ex > 0
2. ex > 1 for x> 0
3. ex > 1+ x
Proofs. We will take property 1 (ex > 0) for granted. Proofs of the other two properties follow:
Proof of 2: Define f (x)= ex −1. Then, f (0) = e0 −1 = 0, and f�(x)= ex > 0. (This last assertion
1 1 1
is from step 1). Hence, f (x) is increasing, so f(x) >f(0) for x> 0. That is:
1
ex > 1 for x> 0
.
Proof of 3: Let f (x)= ex− (1 + x).
2
f�(x)= e x − 1= f (x) > 0 (if x> 0).
2 1
Hence, f (x) > 0 for x> 0. In other words,
2
e x > 1+ x
x2 x2
Similarly, e x > 1+ x + (proved using f (x)= e x − (1 + x + )). One can keep on going:
2 3 2
x2 x3
e x > 1+ x + + for x> 0. Eventually, it turns out that
2 3!
x2 x3
ex =1+ x + + + ··· (an infinite sum)
2 3!
We will be discussing this when we get to Taylor series near the end of the course.
4

Lecture 15 18.01 Fall 2006
Lecture 15: Differentials and Antiderivatives
Differentials
New notation:
dy = f�(x)dx (y = f(x))
Both dy and f�(x)dx are called differentials. You can think of
dy
= f�(x)
dx
as a quotient of differentials. One way this is used is for linear approximations.
Δy dy
≈
Δx dx
Example 1. Approximate 651/3
Method 1 (review of linear approximation method)
f(x) = x 1/3
1
f�(x) = x−2/3
3
f(x) ≈ f(a)+ f�(a)(x − a)
1
x 1/3 ≈ a1 /3 + a−2/3(x − a)
3
A good base point is a = 64, because 641/3 = 4.
Let x = 65.
� �
1 1 1 1
651/3 = 641/3 + 64−2/3(65 − 64)=4+ (1)=4+ ≈ 4.02
3 3 16 48
Similarly,
1
(64.1)1/3 ≈ 4+
480
Method 2 (review)
1 1
�
1
�1/3
651/3 = (64 + 1)1/3 = [64(1 + )]1/3 = 641/3[1+ ]1/3 =4 1+
64 64 64
1 1
Next, use the approximation (1 + x)r ≈ 1+ rx with r = and x = .
3 64
1 1 1
651/3 ≈ 4(1+ ( ))=4+
3 64 48
This is the same result that we got from Method 1.
1

Lecture 15 18.01 Fall 2006
Method 3 (with differential notation)
y = x1 /3| =4
x=64
� �
1 1 1 1
dy = x−2/3dx| = dx = dx
3 x=64 3 16 48
1
We want dx = 1, since (x + dx) = 65. dy = when dx = 1.
48
1
(65)1/3 =4+
48
What underlies all three of these methods is
y = x1 /3
dy 1
= x−2/3|
dx 3 x=64
Anti-derivatives
�
F (x)= f(x)dx means that F is the antiderivative of f.
Other ways of saying this are:
F �(x)= f(x) or, dF = f(x)dx
Examples:
�
1. sin xdx = − cos x + c where c is any constant.
� xn+1
2. x ndx = + c for n �= −1.
n +1
� dx
3. = ln |x| + c (This takes care of the exceptional case n = −1 in 2.)
x
�
4. sec2 xdx = tan x + c
� dx 1
5. √ = sin−1 x + c (where sin−1 x denotes “inverse sin” or arcsin, and not )
1 − x2 sin x
� dx
6. = tan−1(x)+ c
1+ x2
Proof of Property 2: The absolute value |x| gives the correct answer for both positive and negative
x. We will double check this now for the case x< 0:
ln |x| = ln(−x)
� �
d d du
ln(−x) = ln(u) where u = −x.
dx du dx
d 1 1 1
ln(−x) = (−1) = (−1) =
dx u −x x
2

Lecture 15 18.01 Fall 2006
Uniqueness of the antiderivative up to an additive constant.
If F �(x)= f(x), and G�(x)= f(x), then G(x)= F (x)+ c for some constant factor c.
Proof:
(G − F )� = f − f =0
Recall that we proved as a corollary of the Mean Value Theorem that if a function has a derivative
zero then it is constant. Hence G(x) − F (x)= c (for some constant c). That is, G(x)= F (x)+ c.
Method of substitution.
�
Example 1. x 3(x 4 + 2)5dx
Substitution:
1
u = x4 +2, du =4x3 dx, (x 4 + 2)5 = u5 , x3 dx = du
4
Hence,
� 1 � u6 u6 1
x 3(x 4 + 2)5dx = u5 du = = + c = (x4 + 2)6 + c
4 4(6) 24 24
� x
Example 2. √ dx
1+ x2
Another way to find an anti-derivative is “advanced guessing.” First write
� x �
√ dx = x(1 + x2 )−1/2dx
1+ x2
Guess: (1 + x2 )1/2 . Check this.
d 1
(1 + x 2)1/2 = (1+ x2 )−1/2(2x)= x(1 + x 2)−1/2
dx 2
Therefore,
�
x(1 + x 2)−1/2dx = (1+ x2 )1/2 + c
�
Example 3. e 6xdx
Guess: e6 x . Check this:
d
e 6x =6e6 x
dx
Therefore,
� 1
e 6xdx = e6 x + c
6
3

Lecture 15 18.01 Fall 2006
�
Example 4. xe−x 2 dx
Guess:
e−x2
Again, take the derivative to check:
d
e−x2 =(−2x)(e−x 2 )
dx
Therefore,
� 1
xe−x 2 dx = − e−x 2 + c
2
� 1
Example 5. sin x cos xdx = sin2 x + c
2
Another, equally acceptable answer is
� 1
sin x cos xdx = − cos2 x + c
2
This seems like a contradiction, so let’s check our answers:
d
sin2 x = (2 sin x)(cos x)
dx
and
d
cos2 x = (2 cos x)(− sin x)
dx
So both of these are correct. Here’s how we resolve this apparent paradox: the difference between
the two answers is a constant.
1 1 1 1
sin2 x − (− cos2 x) = (sin2 x + cos2 x)=
2 2 2 2
So,
1 1 1 1 1
sin2 x − = (sin2 x − 1)= (− cos2 x)= − cos2 x
2 2 2 2 2
The two answers are, in fact, equivalent. The constant c is shifted by 1 from one answer to the
2
other.
� dx
Example 6. (We will assume x> 0.)
x ln x
1
Let u = ln x. This means du = dx. Substitute these into the integral to get
x
� dx � 1
= du = ln u + c = ln(ln(x)) + c
x ln x u
4

Lecture 16 18.01Fall 2006
Lecture 16: Differential Equations and Separation
of Variables
Ordinary Differential Equations (ODEs)
dy
Example 1. = f(x)
dx
�
Solution: y = f(x)dx. We consider these types of equations as solved.
� � � �
d dy
Example 2. + x y =0 or + xy =0
dx dx
� �
d
( + x is known in quantum mechanics as the annihilation operator.)
dx
Besides integration, we have only one method of solving this so far, namely, substitution. Solving
dy
for gives:
dx
dy
= −xy
dx
The key step is to separate variables.
dy
= −xdx
y
Note that all y-dependence is on the left and all x-dependence is on the right.
Next, take the antiderivative of both sides:
� dy �
= − xdx
y
x2
ln |y| = − + c (only need one constant c)
2
|y| = ec e−x2 /2 (exponentiate)
y = ae−x2/2 (a = ±e c)
Despite the fact that ec =� 0,a = 0 is possible along with all a �= 0, depending on the initial
conditions. For instance, if y(0) = 1, then y = e−x 2/2 . If y(0) = a, then y = ae−x 2/2 (See Fig. 1).
1

1
0.8
0.6
0.4
0.2
0
−6 −4 −2 0 2 4 6
X
� �
Y
Lecture 16 18.01Fall 2006
Figure 1: Graph of y = e− x 2 2 .
In general:
dy
= f(x)g(y)
dx
dy
= f(x)dx which we can write as
g(y)
1
h(y)dy = f(x)dx where h(y)= .
g(y)
Now, we get an implicit formula for y:
H(y)= F (x)+ c (H(y)= h(y)dy; F (x)= f(x)dx)
where H� = h, F � = f, and
y = H−1(F (x)+ c)
(H−1 is the inverse function.)
In the previous example:
−x2
f(x) = x; F (x)= ;
2
1 1
g(y) = y; h(y)= = , H(y) = ln |y|
g(y) y
2

Lecture 16 18.01Fall 2006
dy �y �
Example 3 (Geometric Example). =2 .
dx x
Find a graph such that the slope of the tangent line is twice the slope of the ray from (0, 0) to (x,y)
seen in Fig. 2.
(x,y)
Figure 2: The slope of the tangent line (red) is twice the slope of the ray from the origin to the point (x,y).
dy 2dx
= (separate variables)
y x
ln |y| = 2 ln |x| + c (antiderivative)
|y| = e c x 2 (exponentiate; remember, e 2 ln |x| = x2 )
Thus,
y = ax2
Again, a< 0, a> 0 and a = 0 are all acceptable. Possible solutions include, for example,
y = x2 (a = 1)
y = 2x2 (a = 2)
y = −x 2 (a = −1)
y = 0x2 =0 (a = 0)
y = −2y 2 (a = −2)
y = 100x2 (a = 100)
3

Lecture 16 18.01Fall 2006
Example 4. Find the curves that are perpendicular to the parabolas in Example 3.
We know that their slopes,
dy −1 −x
= =
dx slope of parabola 2y
Separate variables:
−x
ydy = dx
2
Take the antiderivative:
y2 x2 x2 y2
= − + c =⇒ + = c
2 4 4 2
which is an equation for a family of ellipses. For these ellipses, the ratio of the x-semi-major axis to
√
the y-semi-minor axis is 2 (see Fig. 3).
Figure 3: The ellipses are perpendicular to the parabolas.
Separation of variables leads to implicit formulas for y, but in this case you can solve for y.
�
� x2 �
y = ± 2 c −
4
Exam Review
Exam 2 will be harder than exam 1 — be warned! Here’s a list of topics that exam 2 will cover:
1. Linear and/or quadratic approximations
2. Sketches of y = f(x)
3. Maximum/minimum problems.
4. Related rates.
5. Antiderivatives. Separation of variables.
6. Mean value theorem.
More detailed notes on all of these topics are provided in the Exam 2 review sheet.
4

18.01 UNIT 2 REVIEW; Fall 2007
The central theme of Unit 2 is that knowledge of f
�
(and sometimes f
��
) tells us something about
f itself. This is even true of our first topic, approximation. For instance, knowing that f(x) = e
x
�
satisfies f(0) = 1 and f (0) = 1, we can say
e x � 1+ x provided x � 0
x �
The linear function 1 + x is much simpler than e , so f(0) and f (0) give us a (very) simplified
picture of our function, useful only near near 0. For more detail, use the quadratic approximation,
e x � 1+ x + x 2 /2 provided x � 0
(still only works well near 0)
The second and third practice exams are actual tests from previous years. The exam this year
is similar to the one from 2006 posted at our site. It has 6 questions covering the following topics.
(No Newton’s method, but there is a seventh, extra credit problem.)
1. Linear and/or quadratic approximations
2. Sketch a graph y = f(x)
3. Max/min
4. Related rates
5. Find antiderivatives and solve a differential equation by separating variables
6. Mean value theorem.
Remarks.
1. Recall that linear [and quadratic] approximation is
f(x) � f(a)+ f � (a)(x − a) [+(f �� (a)/2)(x − a) 2 ]
2. You should expect to graph a function y = f(x), where f(x) is a rational function (ratio of
polynomials).
Warnings:
a) When asked to label the critical point on the graph, find and mark the point (a,b). In lecture
we called x = a the critical point and y = b the critical value, and this is what is used in 18.02,
and elsewhere. But for this exam (and this is just an inconsistency in language that you will have
to tolerate) the words “critical point” refer to the point on the graph (a,b), not the number a and
the point on the x-axis. The same applies to inflection points.
b) y = 1/(x − 1) is decreasing on the intervals −≈ < x < 1 and 1 < x < ≈, but it is not
decreasing on the interval −≈ < x < ≈. Draw the graph to see.
You cannot just use the fact that y � = −1/(x − 1) 2 < 0 because there is a point in the middle
at which y is not differentiable — and not even continuous. So the mean value theorem does not
apply.
c) Similarly, y = 1/(x − 1) 2 is concave up on −≈ < x < 1 and 1 < x < ≈, but it is not
concave up on the interval −≈ < x < ≈. Here y �� = 6/(x − 1) 4 > 0, but there is a singularity in
the middle. Plot the graph yourself to see.
1

3. The mean value theorem says that if f is differentiable, then for some c, a < c < x,
�
f(x) = f(a)+ f (c)(x − a)
�
It is used as follows. Suppose that m <f (c) < M on the interval a < c < x, then
f(x) = f(a)+ f � (c)(x − a) < f(a)+ M(x − a)
Similarly,
f(x) = f(a)+ f � (c)(x − a) > f(a)+ m(x − a)
Put another way, if �f = f(x) − f(a) and �x = x − a, and m < f � (c) < M for a <c < x, then
m�x < �f < M�x
More consequences of the mean value theorem.
A function f is called increasing (also called strictly increasing) if x > a implies f(x) > f(a).
The reasoning above with m = 0 shows that if f
�
> 0, then f is increasing. Similarly if f
�
< 0, then
f is decreasing. We use these facts every time we sketch a graph of a function or find a maximum
or minimum.
A similar discussion works when the inequality is not strict. If m � f � (c) � M for a < c < x,
then
f(a)+ m(x − a) � f(x) � f(a)+ M(x − a)
A function is called nondecreasing if x > a implies f(x) � f(a). If f � � 0, then the inequality
above shows that f is nondecreasing. Conversely, if the function is nondecreasing and differentiable,
then f � � 0. Similarly, differentiable functions are nonincreasing if and only if they satisfy f � � 0.
Key corollary to the mean value theorem: f � = g � implies f − g is constant.
In Unit 2, we have found that information about f
�
gives information about f. In particular,
knowing a starting value for a function and its rate of change determines the function. A seemingly
obvious example is that if f
�
= 0 for all x, then f is constant. If this were not true, then the
mathematical notion of derivative would fail to coincide with our intuitive notion of what rate of
change and cause and effect mean.
But this fundamental fact needs a proof. Derivatives are instantaneous quantities, obtained
as limits. It is the mean value theorem that allows us to pass in rigorous mathematical fashion
from the infinitesimal to the practical, human scale. Here is the proof. If f
�
= 0, then one can
take m = M = 0 in the inequalities above, and conclude that f(x) = f(a). In other words, f is
constant. As an immediate consequence, if f
�
= g
�
, then f and g differ by a constant. (Apply the
previous argument to the function f − g, whose derivative is 0.) This basic fact will lead us shortly
to what is known as the fundamental theorem of calculus.
2

