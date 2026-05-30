# MIT 18.01 Single Variable Calculus — Unit 3: The Definite Integral and Its Applications

> Source: MIT OpenCourseWare, http://ocw.mit.edu
> Collected: 2026-05-29
> Published: Fall 2006

MIT OpenCourseWare
http://ocw.mit.edu
18.01 Single Variable Calculus
Fall 2006
For information about citing these materials or our Terms of Use, visit: http://ocw.mit.edu/terms.

Lecture 18 18.01 Fall 2006
Lecture 18: Definite Integrals
Integrals are used to calculate cumulative totals, averages, areas.
Area under a curve: (See Figure 1.)
1. Divide region into rectangles
2. Add up area of rectangles
3. Take limit as rectangles become thin
a b a b
(i) (ii)
Figure 1: (i) Area under a curve; (ii) sum of areas under rectangles
Example 1. f(x)= x2 , a = 0, b arbitrary
1. Divide into n intervals
Length b/n = base of rectangle
2. Heights:
b
�
b
�2
• 1st: x = , height =
n n
2b
�
2b
�2
• 2nd: x = , height =
n n
Sum of areas of rectangles:
� b �� b �2 � b �� 2b �2 � b �� 3b �2 � b �� nb �2 b3
+ + +··· + = (12 +22 +32 +··· + n2 )
n n n n n n n n n3
1

Lecture 18 18.01 Fall 2006
a=0 b
Figure 2: Area under f (x)= x2 above [0,b].
We will now estimate the sum using some 3-dimensional geometry.
Consider the staircase pyramid as pictured in Figure 3.
n = 4
n
Figure 3: Staircase pyramid: left(top view) and right (side view)
1st level: n × n bottom, represents volume n2 .
2nd level: (n − 1) × (n − 1), represents volumne (n − 1)2), etc.
Hence, the total volume of the staircase pyramid is n2 +(n − 1)2 + ··· +1.
Next, the volume of the pyramid is greater than the volume of the inner prism:
1 1 1
12 +22 +··· + n2 > (base)(height) = n2 · n = n3
3 3 3
and less than the volume of the outer prism:
1 1
12 +22 +··· + n2 < (n + 1)2(n +1)= (n + 1)3
3 3
2

Lecture 18 18.01 Fall 2006
In all,
1 1 n3 12 +22 +··· + n2 1(n + 1)3
= 3 < <
3 n3 n3 3 n3
Therefore,
b3 1
lim (12 +22 +32 +··· + n2 )= b3 ,
n→∞ n3 3
b3
and the area under x2 from 0 to b is .
3
Example 2. f(x)= x; area under x above [0,b]. Reasoning similar to Example 1, but easier, gives
a sum of areas:
b2 1
(1 + 2 + 3 + ··· + n) → b2 (as n →∞)
n2 2
This is the area of the triangle in Figure 4.
b
b
Figure 4: Area under f (x)= x above [0,b].
Pattern:
d � b3 �
= b2
db 3
d � b2 �
= b
db 2
The area A(b) under f(x) should satisfy A�(b)= f(b).
3

Lecture 18 18.01 Fall 2006
General Picture
y=f(x)
a c b
i
Figure 5: One rectangle from a Riemann Sum
b − a
• Divide into n equal pieces of length = Δx =
n
• Pick any c in the interval; use f(c ) as the height of the rectangle
i i
• Sum of areas: f(c )Δx + f(c )Δx + ··· + f(c )Δx
1 2 n
n
�
In summation notation: f(c )Δx ← called a Riemann sum.
i
i=1
Definition:
n � b
�
lim f(c )Δx = f(x)dx ← called a definite integral
i
n→∞
i=1 a
This definite integral represents the area under the curve y = f(x) above [a,b].
Example 3. (Integrals applied to quantity besides area.) Student borrows from parents.
P = principal in dollars, t = time in years, r = interest rate (e.g., 6 % is r =0.06/year).
After time t, you owe P (1 + rt)= P + Prt
The integral can be used to represent the total amount borrowed as follows. Consider a function
f(t), the “borrowing function” in dollars per year. For instance, if you borrow $ 1000 /month, then
f(t) = 12, 000/year. Allow f to vary over time.
Say Δt =1/12 year = 1 month.
t = i/12 i =1, ··· , 12.
i
4

Lecture 18 18.01 Fall 2006
f(t ) is the borrowing rate during the ith month so the amount borrowed is f(t )Δt. The total is
i i
12
�
f(t )Δt.
i
i=1
In the limit as Δt → 0, we have
� 1
f(t)dt
0
which represents the total borrowed in one year in dollars per year.
The integral can also be used to represent the total amount owed. The amount owed depends
on the interest rate. You owe
f(t )(1 + r(1 − t ))Δt
i i
for the amount borrowed at time t . The total owed for borrowing at the end of the year is
i
� 1
f(t)(1 + r(1 − t))dt
0
5

Lecture 19 18.01 Fall 2006
Lecture 19: First Fundamental Theorem of
Calculus
Fundamental Theorem of Calculus (FTC 1)
If f(x) is continuous and F �(x)= f(x), then
� b
f(x)dx = F (b) − F (a)
a
�b �x=b
Notation: F (x) � = F (x) � = F (b) − F (a)
� �
a x=a
Example 1. F (x)=
x3
, F �(x)= x 2;
� b
x 2dx =
x3 �
� �
b
=
b3
−
a3
3 3 � 3 3
a a
Example 2. Area under one hump of sin x (See Figure 1.)
� π �π
sin xdx = − cos x � = − cos π − (− cos0) = −(−1) − (−1) = 2
�
0 0
1
�
Figure 1: Graph of f (x) = sin x for 0 ≤ x ≤ π.
Example 3. � 1 x 5dx = x6 � � � 1 = 1 − 0= 1
6 � 6 6
0 0
1

Lecture 19 18.01 Fall 2006
Intuitive Interpretation of FTC:
dx
x(t) is a position; v(t)= x�(t) = is the speed or rate of change of x.
dt
� b
v(t)dt = x(b) − x(a) (FTC 1)
a
R.H.S. is how far x(t) went from time t = a to time t = b (difference between two odometer readings).
L.H.S. represents speedometer readings.
n
�
v(t )Δt approximates the sum of distances traveled over times Δt
i
i=1
The approximation above is accurate if v(t) is close to v(t ) on the ith interval. The interpretation
i
of x(t) as an odometer reading is no longer valid if v changes sign. Imagine a round trip so that
x(b) − x(a) = 0. Then the positive and negative velocities v(t) cancel each other, whereas an
odometer would measure the total distance not the net distance traveled.
� 2π �2π
Example 4. sin xdx = − cos x � = − cos2π − (− cos0) = 0.
�
0 0
The integral represents the sum of areas under the curve, above the x-axis minus the areas below
the x-axis. (See Figure 2.)
1
+
2�
-
Figure 2: Graph of f(x) = sin x for 0 ≤ x ≤ 2π.
2

Lecture 19 18.01 Fall 2006
Integrals have an important additive property (See Figure 3.)
� b � c � c
f(x)dx + f(x)dx = f(x)dx
a b a
a b c
Figure 3: Illustration of the additive property of integrals
New Definition:
� a � b
f(x)dx = − f(x)dx
b a
This definition is used so that the fundamental theorem is valid no matter if a<b or b<a. It also
makes it so that the additive property works for a,b,c in any order, not just the one pictured in
Figure 3.
3

Lecture 19 18.01 Fall 2006
Estimation:
� b � b
If f(x) ≤ g(x), then f(x)dx ≤ g(x)dx (only if a<b)
a a
Example 5. Estimation of ex
Since 1 ≤ ex for x ≥ 0,
� 1 � 1
1dx ≤ e xdx
0 0
� 1 � 1
ex dx = ex � = e1 − e 0 = e − 1
�
0 0
Thus 1 ≤ e − 1, or e ≥ 2.
Example 6. We showed earlier that 1 + x ≤ ex. It follows that
� 1 � 1
(1 + x)dx ≤ e xdx = e − 1
0 0
� 1 � x2 � � � 1 3
(1 + x)dx = x + � =
2 � 2
0 0
3 5
Hence, ≤ e − 1,or, e ≥ .
2 2
Change of Variable:
If f(x)= g(u(x)), then we write du = u�(x)dx and
� � �
g(u)du = g(u(x))u�(x)dx = f(x)u�(x)dx (indefinite integrals)
For definite integrals:
� x2 � u2
f(x)u�(x)dx = g(u)du where u = u(x ), u = u(x )
1 1 2 2
x1 u1
� 2
Example 7. � x 3 +2 �4 x2 dx
1
du
Let u = x3 +2. Then du =3x2 dx =⇒ x2 dx = ;
3
x =1,x =2 =⇒ u =13 +2=3, u =23 +2 = 10, and
1 2 1 2
� 2 � x 3 +2 �4 x2 dx = � 10 u 4 du = u5 � � � 10 = 105 − 35
3 15 � 15
1 3 3
4

Lecture 20 18.01 Fall 2006
Lecture 20: Second Fundamental Theorem
Recall: First Fundamental Theorem of Calculus (FTC 1)
If f is continuous and F � = f, then
� b
f(x)dx = F (b) − F (a)
a
We can also write that as
� b � �x=b
f(x)dx = f(x)dx �
�
a x=a
Do all continuous functions have antiderivatives? Yes. However...
What about a function like this?
�
e−x 2 dx =??
Yes, this antiderivative exists. No, it’s not a function we’ve met before: it’s a new function.
The new function is defined as an integral:
� x
F (x)=
e−t2
dt
0
It will have the property that F �(x)= e−x 2 .
sin x
Other new functions include antiderivatives of e−x 2 ,x1 /2e−x 2 , , sin(x 2), cos(x 2),...
x
Second Fundamental Theorem of Calculus (FTC 2)
� x
If F (x)= f(t)dt and f is continuous, then
a
F �(x)= f(x)
Geometric Proof of FTC 2: Use the area interpretation: F (x) equals the area under the curve
between a and x.
ΔF = F (x +Δx) − F (x)
ΔF ≈ (base)(height) ≈ (Δx)f(x) (See Figure 1.)
ΔF
≈ f(x)
Δx
ΔF
Hence lim = f(x)
Δx→0 Δx
But, by the definition of the derivative:
ΔF
lim = F �(x)
Δx→0 Δx
1

Lecture 20 18.01 Fall 2006
y
∆F
F(x)
a x x+∆x
Figure 1: Geometric Proof of FTC 2.
Therefore,
F �(x)= f(x)
Another way to prove FTC 2 is as follows:
� �
ΔF 1 � x+Δx � x
= f(t)dt − f(t)dt
Δx Δx
a a
1 � x+Δx
= f(t)dt (which is the “average value” of f on the interval x ≤ t ≤ x +Δx.)
Δx
x
As the length Δx of the interval tends to 0, this average tends to f(x).
Proof of FTC 1 (using FTC 2)
� x
Start with F � = f (we assume that f is continuous). Next, define G(x)= f(t)dt. By FTC2,
a
G�(x) = f(x). Therefore, (F − G)� = F � − G� = f − f = 0. Thus, F − G = constant. (Recall we
used the Mean Value Theorem to show this).
Hence, F (x)= G(x)+ c. Finally since G(a) = 0,
� b
f(t)dt = G(b)= G(b) − G(a)=[F (b) − c] − [F (a) − c]= F (b) − F (a)
a
which is FTC 1.
Remark. In the preceding proof G was a definite integral and F could be any antiderivative. Let
us illustrate with the example f(x) = sin x. Taking a = 0 in the proof of FTC 1,
� x � x
G(x) = cos tdt = sin t� = sin x and G(0) = 0.
�
0 0
2

Lecture 20 18.01 Fall 2006
If, for example, F (x) = sin x + 21. Then F �(x) = cos x and
� b
sin xdx = F (b) − F (a) = (sin b + 21) − (sin a + 21) = sin b − sin a
a
Every function of the form F (x)= G(x)+ c works in FTC 1.
Examples of “new” functions
The error function, which is often used in statistics and probability, is defined as
2 � x
erf(x) = √ e−t2 dt
π
0
and lim erf(x) = 1 (See Figure 2)
x→∞
Figure 2: Graph of the error function.
Another “new” function of this type, called the logarithmic integral, is defined as
� x dt
Li(x)=
ln t
2
This function gives the approximate number of prime numbers less than x. A common encryption
technique involves encoding sensitive information like your bank account number so that it can be
sent over an insecure communication channel. The message can only be decoded using a secret
prime number. To know how safe the secret is, a cryptographer needs to know roughly how many
200-digit primes there are. You can find out by estimating the following integral:
� 10201 dt
ln t
10200
We know that
ln10200 = 200 ln(10) ≈ 200(2.3) = 460 and ln10201 = 201 ln(10) ≈ 462
3

Lecture 20 18.01 Fall 2006
We will approximate to one significant figure: ln t ≈ 500 for 200 ≤ t ≤ 10201 .
With all of that in mind, the number of 200-digit primes is roughly 1
� 10201 dt ≈ � 10201 dt = 1 � 10201 − 10200� ≈ 9 · 10200 ≈ 10198
ln t 500 500 500
10200 10200
There are LOTS of 200-digit primes. The odds of some hacker finding the 200-digit prime required
to break into your bank account number are very very slim.
Another set of “new” functions are the Fresnel functions, which arise in optics:
� x
C(x) = cos(t2)dt
0
� x
S(x) = sin(t2)dt
0
Bessel functions often arise in problems with circular symmetry:
1 � π
J (x) = cos(x sin θ)dθ
0 2π
0
On the homework, you are asked to find C�(x). That’s easy!
C�(x) = cos(x 2)
� x dt
We will use FTC 2 to discuss the function L(x) = from first principles next lecture.
t
1
1 The middle equality in this approximation is a very basic and useful fact
� b
cdx = c(b − a)
a
Think of this as finding the area of a rectangle with base (b − a) and height c. In the computation above, a =
10200,b = 10201,c = 1
500
4

Lecture 21 18.01 Fall 2006
Lecture 21: Applications to Logarithms and
Geometry
Application of FTC 2 to Logarithms
The integral definition of functions like C(x), S(x) of Fresnel makes them nearly as easy to use as
elementary functions. It is possible to draw their graphs and tabulate values. You are asked to
carry out an example or two of this on your problem set. To get used to using definite integrals
and FTC2, we will discuss in detail the simplest integral that gives rise to a relatively new function,
namely the logarithm.
Recall that
� xn+1
x ndx = + c
n +1
except when n = −1. It follows that the antiderivative of 1/x is not a power, but something else.
So let us define a function L(x) by
� x dt
L(x)=
t
1
(This function turns out to be the logarithm. But recall that our approach to the logarithm was fairly
involved. We first analyzed ax, and then defined the number e, and finally defined the logarithm as
the inverse function to ex. The direct approach using this integral formula will be easier.)
All the basic properties of L(x) follow directly from its definition. Note that L(x) is defined for
0 < x < ∞. (We will not extend the definition past x = 0 because 1/t is infinite at t = 0.) Next,
the fundamental theorem of calculus (FTC2) implies
1
L�(x)=
x
Also, because we have started the integration with lower limit 1, we see that
� 1 dt
L(1)= =0
t
1
Thus L is increasing and crosses the x-axis at x = 1: L(x) < 0 for 0 < x < 1 and L(x) > 0 for
x> 1. Differentiating a second time,
L��(x)= −1/x2
It follows that L is concave down.
The key property of L(x) (showing that it is, indeed, a logarithm) is that it converts multiplication
into addition:
Claim 1. L(ab)= L(a)+ L(b)
Proof: By definition of L(ab) and L(a),
� ab dt � a dt � ab dt � ab dt
L(ab)= = + = L(a)+
t t t t
1 1 a a
1

Lecture 21 18.01 Fall 2006
� ab dt
To handle , make the substitution t = au. Then
t
a
dt = adu; a < t < ab =⇒ 1 <u<b
Therefore,
� ab dt � u=b adu � b du
= = = L(b)
t au u
a u=1 1
This confirms L(ab)= L(a)+ L(b).
Two more properties, the end values, complete the general picture of the graph.
Claim 2. L(x) →∞ as x →∞.
Proof: It suffices to show that L(2n) → ∞ as n → ∞, because the fact that L is increasing fills in
all the values in between the powers of 2.
L(2n) = L(2 · 2n−1)= L(2) + L(2n−1)
= L(2) + L(2) + L(2n−2)= L(2) + L(2)+ ··· + L(2) (n times)
Consequently, L(2n)= nL(2) →∞ as n →∞. (In more familiar notation, ln 2n = n ln2.)
Claim 3. L(x) → −∞ as x → 0+ .
� �
1
Proof: 0 = L(1) = L x · = L(x)+ L(1/x) =⇒ L(x) = −L(1/x). As x → 0+, 1/x → +∞, so
x
Claim 2 implies L(1/x) →∞. Hence
L(x)= −L(1/x) → −∞, as x → 0+
Thus L(x), defined on 0 < x < ∞ increases from −∞ to ∞, crossing the x-axis at x = 1. It is
concave down and its graph can be drawn as in Fig. 1.
This provides an alternative to our previous approach to the exponential and log functions.
Starting from L(x), we can define the log function by ln x = L(x), define e as the number such that
L(e) = 1, define ex as the inverse function of L(x), and define a x = ex L(a).
to +∞
.
(1,0)
to −∞
Figure 1: Graph of y = ln(x).
2

Lecture 21 18.01 Fall 2006
Application of FTCs to Geometry (Volumes and Areas)
1. Areas between two curves
f(x)
y g(x)
dx
a b
Figure 2: Finding the area between two curves.
Refer to Figure 2. Find the crossing points a and b. The area, A, between the curves is
� b
A = (f(x) − g(x)) dx
a
Example 1. Find the area in the region between x = y2 and y = x − 2.
(4, 2)
x = y2
y = x − 2
(0, 0)
(1,−1)
(0, -2)
Figure 3: The intersection of x = y2 and y = x − 2.
3

Lecture 21 18.01 Fall 2006
First, graph these functions and find the crossing points (see Figure 3).
y +2 = x = y 2
y 2 − y − 2 = 0
(y − 2)(y +1) = 0
Crossing points at y = −1, 2. Plug these back in to find the associated x values, x = 1 and x = 4.
Thus the curves meet at (1, −1) and (4, 2) (see Figure 3).
There are two ways of finding the area between these two curves, a hard way and an easy way.
Hard Way: Vertical Slices
If we slice the region between the two curves vertically, we need to consider two different regions.
(4, 2)
x = y2
dx
y = x − 2
(0, 0)
(1,−1)
(0, -2)
Figure 4: The intersection of x = y2 and y = x − 2.
Where x > 1, the region’s lower bound is the straight line. For x < 1, however, the region’s lower
bound is the lower half of the sideways parabola. We find the area, A, between the two curves by
integrating the difference between the top curve and the bottom curve in each region:
� 1 √ √ � 4 √ �
� � � �
A = x − (− x) dx + x − (x − 2) dx = (y − y ) dx
top bottom
0 1
Easy Way: Horizontal Slices
Here, instead of subtracting the bottom curve from the top curve, we subtract the right curve from
the left one.
A = � (x
left
−x
right
) dy = �
y=
y=
−
2
1
� (y + 2) − y 2� dx = � y
2
2 +2y + −
3
y 3 �� �
�
2
− 1
= 4
2
+4−
3
8 −(
2
1 −2+
3
1 )=
2
9
4

Lecture 21 18.01 Fall 2006
(4, 2)
x = y2
dy y = x − 2 ; (x = y +2)
(0, 0)
(1,−1)
(0, -2)
Figure 5: The intersection of x = y2 and y = x − 2.
2. Volumes of solids of revolution
Rotate f(x) about the x-axis, coming out of the page, to get:
rotate an x-y plane section
y
by 2π radians
f(x)
dx
x
z
Figure 6: A solid of revolution: the purple slice is rotated by π/4 and π/2.
We want to figure out the volume of a “slice” of that solid. We can approximate each slice as a
disk with width dx, radius y, and a cross-sectional area of πy2 . The volume of one slice is then:
dV = πy2dx (for a solid of revolution around the x-axis)
Integrate with respect to x to find the total volume of the solid of revolution.
5

Lecture 21 18.01 Fall 2006
Example 2. Find the volume of a ball of radius a.
y
a
−a a x
dx
Figure 7: A ball of radius a
The equation for the upper half of the circle is
�
y = a2 − x2 .
If we spin the upper part of the curve about the x-axis, we get a ball of radius a. Notice that x
ranges from −a to +a. Putting all this together, we find
� � x=a � πx3 ��a 2 � 2 � 4
V = πy2dx = π(a2 − x 2)dx = πa2 x − � = πa3 − − πa3 = πa3
x=−a 3 � −a 3 3 3
One can often exploit symmetry to further simplify these types of problems. In the problem
above, for example, notice that the curve is symmetric about the y-axis. Therefore,
� a � a � x3��a
V = π(a2 − x 2)dx =2 π(a2 − x2 )dx =2 πa2 x − �
−a 0 3 � 0
(The savings is that zero is an easier lower limit to work with than −a.) We get the same answer:
� x3 ��a � π � 4
V =2 πa2 x − � =2 πa3 − a3 = πa3
3 � 0 3 3
6

Lecture 22 18.01 Fall 2006
Lecture 22: Volumes by Disks and Shells
Disks and Shells
We will illustrate the 2 methods of finding volume through an example.
Example 1. A witch’s cauldron
y
x
Figure 1: y = x2 rotated around the y-axis.
Method 1: Disks
y
a
thickness of dy
x
Figure 2: Volume by Disks for the Witch’s Cauldron problem.
The area of the disk in Figure 2 is πx2 . The disk has thickness dy and volume dV = πx2dy.
The volume V of the cauldron is
� a
V = πx2 dy (substitute y = x2 )
0
� a y2 � a πa2
V = πy dy = π � =
0 2 � 0 2
1

Lecture 22 18.01 Fall 2006
π
If a = 1 meter, then V = a2 gives
2
π π π
V = m 3 = (100 cm)3 = 106 cm3 ≈ 1600 liters (a huge cauldron)
2 2 2
Warning about units.
If a = 100 cm, then
π π π
V = (100)2 = 104 cm3 = 10 ∼ 16 liters
2 2 2
But 100cm = 1m. Why is this answer different? The resolution of this paradox is hiding in the
equation.
y = x2
At the top, 100 = x2 =⇒ x = 10 cm. So the second cauldron looks like Figure 3. By contrast, when
mc
001
20 cm
Figure 3: The skinny cauldron.
a = 1 m, the top is ten times wider: 1 = x2 or x = 1 m. Our equation, y = x2, is not scale-invariant.
The shape described depends on the units used.
Method 2: Shells
This really should be called the cylinder method.
y
x
a
x
√a
Figure 4: x = radius of cylinder. Thickness of cylinder = dx. Height of cylinder = a − y = a − x2.
2

Lecture 22 18.01 Fall 2006
The thin shell/cylinder has height a − x2, circumference 2πx, and thickness dx.
dV = (a − x 2)(2πx)dx
√ √
� x= a � a
V = (a − x 2)(2πx)dx =2π (ax − x 3)dx
x=
�
0
x2 x4 �� √ a � a2
0
a2 � � a2 � πa2
= 2π a − � =2π − =2π = (same as before)
2 4 � 0 2 4 4 2
Example 2. The boiling cauldron
Now, let’s fill this cauldron with water, and light a fire under it to get the water to boil (at 100oC).
Let’s say it’s a cold day: the temperature of the air outside the cauldron is 0oC. How much energy
does it take to boil this water, i.e. to raise the water’s temperature from 0oC to 100oC? Assume the
y
70oC
100oC
x
Figure 5: The boiling cauldron (y = a = 1 meter.)
temperature decreases linearly between the top and the bottom (y = 0) of the cauldron:
T = 100 − 30y (degrees Celsius)
Use the method of disks, because the water’s temperature is constant over each horizontal disk. The
total heat required is
� 1
H = T (πx2)dy (units are (degree)(cubic meters))
0
� 1
= (100 − 30y)(πy)dy
0
� 1 �1
= π (100y − 30y 2)dy = π(50y 2 − 10y 3)� = 40π (deg.)m3
�
0 0
How many calories is that?
1 cal
�
100 cm
�3
# of calories = (40π) = (40π)(106) cal = 125 × 103 kcal
cm3 · deg 1m
There are about 250 kcals in a candy bar, so there are about
� �
1
# of calories = candy bar × 103 ≈ 500 candy bars
2
So, it takes about 500 candy bars’ worth of energy to boil the water.
3

Lecture 22 18.01 Fall 2006
R
velocity
Figure 6: Flow is faster in the center of the pipe. It slows– “sticks”– at the edges (i.e. the inner surface of the pipe.)
Example 3. Pipe flow
Poiseuille was the first person to study fluid flow in pipes (arteries, capillaries). He figured out the
velocity profile for fluid flowing in pipes is:
v = c(R2 − r 2)
distance
v = speed =
time
v
cR2
v=c(R2-r2)
r
R
Figure 7: The velocity of fluid flow vs. distance from the center of a pipe of radius R.
The flow through the “annulus” (a.k.a ring) is (area of ring)(flow rate)
area of ring = 2πrdr (See Fig. 8: circumference 2πr, thickness dr)
v is analogous to the height of the shell.
4

Lecture 22 18.01 Fall 2006
r
dr
Figure 8: Cross-section of the pipe.
� R � R
total flow through pipe = v(2πrdr)= c (R2 − r 2)2πrdr
0 0
� R � R2r2 r4 ��R
= 2πc (R2 r − r 3)dr =2πc − �
0 2 4 � 0
π
flow through pipe = cR4
2
Notice that the flow is proportional to R4. This means there’s a big advantage to having thick pipes.
Example 4. Dart board
You aim for the center of the board, but your aim’s not always perfect. Your number of hits, N, at
radius r is proportional to e−r 2.
N = ce−r 2
This looks like:
1
y = ce-r2
r 2
Figure 9: This graph shows how likely you are to hit the dart board at some distance r from its center.
The number of hits within a given ring with r <r <r is
1 2
c
� r2
e−r 2 (2πrdr)
r1
We will examine this problem more in the next lecture.
5

Lecture 23 18.01 Fall 2006
Lecture 23: Work, Average Value, Probability
Application of Integration to Average Value
You already know how to take the average of a set of discrete numbers:
a + a a + a + a
1 2 or 1 2 3
2 3
Now, we want to find the average of a continuum.
y=f(x)
.
y
4
.
a x b
4
Figure 1: Discrete approximation to y = f (x) on a ≤ x ≤ b.
y + y + ... + y
Average ≈ 1 2 n
n
where
a = x <x <··· x = b
0 1 n
y = f(x ), y = f(x ), ...y = f(x )
0 0 1 1 n n
and
b − a
n(Δx)= b − a ⇐⇒ Δx =
n
and
The limit of the Riemann Sums is
b − a � b
lim (y + ··· + y ) = f(x) dx
n→∞ 1 n n
a
Divide by b − a to get the continuous average
y +··· + y 1 � b
lim 1 n = f(x) dx
n→∞ n b − a
a
1

Lecture 23 18.01 Fall 2006
y=√1-x2
area = �/2
Figure 2: Average height of the semicircle.
√
Example 1. Find the average of y = 1 − x2 on the interval −1 ≤ x ≤ 1. (See Figure 2)
1 � 1 � 1 � π � π
Average height = 1 − x2dx = =
2 2 2 4
−1
Example 2. The average of a constant is the same constant
1 � b
53 dx = 53
b − a
a
Example 3. Find the average height y on a semicircle, with respect to arclength. (Use dθ not dx.
See Figure 3)
equal weighting in θ
different weighting in x
Figure 3: Different weighted averages.
2

Lecture 23 18.01 Fall 2006
y = sin θ
1 � π 1 �π 1 2
Average = sin θ dθ = (− cos θ) � = (− cos π − (− cos 0)) =
π 0 π � 0 π π
Example 4. Find the average temperature of water in the witches cauldron from last lecture. (See
Figure 4).
2m
1m
Figure 4: y = x2, rotated about the y-axis.
First, recall how to find the volume of the solid of revolution by disks.
� 1 � 1 πy2 �1 π
V = (πx2) dy = πy dy = � =
0 0 2 � 0 2
Recall that T (y) = 100 − 30y and (T (0) = 100o; T (1) = 70o). The average temperature per unit
volume is computed by giving an importance or “weighting” w(y)= πy to the disk at height y.
�1
T (y)w(y) dy
0
�1
w(y) dy
0
The numerator is
� 1 � 1 �1
T πy dy = π (100 − 30y)ydy = π(500y 2 − 10y 3) � = 40π
�
0 0 0
Thus the average temperature is:
40π
= 80oC
π/2
Compare this with the average taken with respect to height y:
1 � 1 � 1 �1
T dy = (100 − 30y)dy = (100y − 15y 2) � = 85oC
1 0 0 � 0
T is linear. Largest T = 100oC, smallest T = 70oC, and the average of the two is
70 + 100
= 85
2
3

Lecture 23 18.01 Fall 2006
The answer 85o is consistent with the ordinary average. The weighted average (integration with
respect to πy dy) is lower (80o) because there is more water at cooler temperatures in the upper
parts of the cauldron.
Dart board, revisited
Last time, we said that the accuracy of your aim at a dart board follows a “normal distribution”:
ce−r 2
Now, let’s pretend someone – say, your little brother – foolishly decides to stand close to the dart
board. What is the chance that he’ll get hit by a stray dart?
dart board
r₁
3r₁
2r₁
little
brother
Figure 5: Shaded section is 2ri <r< 3r1 between 3 and 5 o’clock.
To make our calculations easier, let’s approximate your brother as a sector (the shaded region
in Fig. 5). Your brother doesn’t quite stand in front of the dart board. Let us say he stands at a
distance r from the center where 2r < r < 3r and r is the radius of the dart board. Note that
1 1 1
your brother doesn’t surround the dart board. Let us say he covers the region between 3 o’clock
1
and 5 o’clock, or of a ring.
6
Remember that
part
probability =
whole
4

Lecture 23 18.01 Fall 2006
width dr,
circumference 2πr
r weighting ce-r2
dr
Figure 6: Integrating over rings.
� �
The ring has weight ce−r 2 (2πr)(dr) (see Figure 6). The probability of a dart hitting your brother
is:
1�3r1 ce−r 2 2πr dr
6 2r1
�∞
ce−r2 2πr dr
0
1 5 − 3
Recall that = is our approximation to the portion of the circumference where the little
6 12
brother stands. (Note: e−r 2 = e(−r 2) not (e−r)2 )
� b 1 �b 1 1 � d �
re−r 2 dr = − e−r 2 � = − e−b2 + e−a2 e−r 2 = −2re−r 2
a 2 � a 2 2 dr
Denominator:
� ∞ 1 �R→∞ 1 1 1
e−r 2 rdr = − e−r 2� = − e−R2 + e−02 =
0 2 � 0 2 2 2
(Note that e−R2 → 0 as R →∞.)
Figure 7: Normal Distribution.
Probability = 1 6
�
�
0 ∞
2 3 r r 1 1
c e
c
−
e−
r2
r
2
2
π
2π
r
r
d r
d r = 1 6
�
�
0 ∞
2 3 r r 1 1
e −
e−
r2
r
r
2 r
d r
d r =
3
1 �
2 r
3
1
r1 e−r 2 r dr = −e
6
−r 2 � �
�
3
2
r
r
1
1
5

Lecture 23 18.01 Fall 2006
−e−9r 1 2 + e−4r 1 2
Probability =
6
Let’s assume that the person throwing the darts hits the dartboard 0 ≤ r ≤ r about half the time.
1
(Based on personal experience with 7-year-olds, this is realistic.)
P (0 ≤ r ≤ r 1 )=
1
2 =
� r1
2e−r 2 rdr = −e−r 1 2 +1 =⇒ e−r1 2 =
1
2
0
1
e−r 1 2 =
2
� �9 � 1 �9
e−9r 1 2 = e−r 1 2 = ≈ 0
2
� �4 � 1 �4 1
e−4r 1 2 = e−r 1 2 = =
2 16
So, the probability that a stray dart will strike your little brother is
� �� �
1 1 1
≈
16 6 100
In other words, there’s about a 1% chance he’ll get hit with each dart thrown.
6

Lecture 23 18.01 Fall 2006
Volume by Slices: An Important Example
� ∞
Compute Q = e−x 2 dx
−∞
Figure 8: Q = Area under curve e(−x 2).
This is one of the most important integrals in all of calculus. It is especially important in probability
and statistics. It’s an improper integral, but don’t let those ∞’s scare you. In this integral, they’re
actually easier to work with than finite numbers would be.
To find Q, we will first find a volume of revolution, namely,
V = volume under e−r 2 (r = � x2 + y2)
We find this volume by the method of shells, which leads to the same integral as in the last problem.
The shell or cylinder under e−r 2 at radius r has circumference 2πr, thickness dr; (see Figure 9).
Therefore dV = e−r 22πrdr. In the range 0 ≤ r ≤ R,
� R �R
e−r 2 2πr dr = −πe−r 2 � = −πe−R2 + π
�
0 0
When R →∞,e−R2 → 0,
� ∞
V = e−r 2 2πr dr = π (same as in the darts problem)
0
7

Lecture 23 18.01 Fall 2006
width dr
r
Figure 9: Area of annulus or ring, (2πr)dr.
Next, we will find V by a second method, the method of slices. Slice the solid along a plane
where y is fixed. (See Figure 10). Call A(y) the cross-sectional area. Since the thickness is dy (see
Figure 11),
� ∞
V = A(y) dy
−∞
z
A(y)
y
x
Figure 10: Slice A(y).
8

Lecture 23 18.01 Fall 2006
y
dy
x
above level of y
in cross-section
of area A(y)
top view
Figure 11: Top view of A(y) slice.
To compute A(y), note that it is an integral (with respect to dx)
� ∞ � ∞ � ∞
A(y)= e−r 2 dx = e−x2 −y 2 dx = e−y 2 e−x2 dx = e−y 2 Q
−∞ −∞ −∞
Here, we have used r2 = x2 + y2 and
e−x 2−y 2 = e−x 2 e−y 2
and the fact that y is a constant in the A(y) slice (see Figure 12). In other words,
� ∞ � ∞
ce−x 2 dx = c e−x 2 dx with c = e−y 2
−∞ −∞
y fixed
ce-x2
x -∞ x ∞
Figure 12: Side view of A(y) slice.
9

Lecture 23 18.01 Fall 2006
It follows that
� ∞ � ∞ � ∞
V = A(y) dy = e−y 2 Qdy = Q e−y 2 dy = Q2
−∞ −∞ −∞
Indeed,
� ∞ � ∞
Q = e−x2 dx = e−y 2 dy
−∞ −∞
because the name of the variable does not matter. To conclude the calculation read the equation
backwards:
√
π = V = Q2 =⇒ Q = π
√
We can rewrite Q = π as
1 � ∞
√ e−x2 dx =1
π
−∞
√
An equivalent rescaled version of this formula (replacing x with x/ 2σ)is used:
1 � ∞
√ e−x 2 /2σ2 dx =1
2πσ
−∞
1
This formula is central to probability and statistics. The probability distribution √ e−x 2/2σ2 on
2πσ
−∞ <x< ∞ is known as the normal distribution, and σ > 0 is its standard deviation.
10

Lecture 24 18.01 Fall 2006
Lecture 24: Numerical Integration
Numerical Integration
We use numerical integration to find the definite integrals of expressions that look like:
� b
(a big mess)
a
We also resort to numerical integration when an integral has no elementary antiderivative. For
instance, there is no formula for
� x � 3
cos(t2)dt or e−x 2 dx
0 0
Numerical integration yields numbers rather than analytical expressions.
We’ll talk about three techniques for numerical integration: Riemann sums, the trapezoidal rule,
and Simpson’s rule.
1. Riemann Sum
a b
Figure 1: Riemann sum with left endpoints: (y0 + y1 + ... + yn−1)Δx
Here,
x − x =Δx
i i−1
(or, x = x +Δx)
i i−1
a = x <x <x < ... < x = b
0 1 2 n
y = f(x ), y = f(x ),...y = f(x )
0 0 1 1 n n
1

Lecture 24 18.01 Fall 2006
2. Trapezoidal Rule
The trapezoidal rule divides up the area under the function into trapezoids, rather than rectangles.
The area of a trapezoid is the height times the average of the parallel bases:
� � � �
base 1+base 2 y + y
Area = height = 3 4 Δx (See Figure 2)
2 2
y
4
y
3
∆x
Figure 2: Area =
�y3 + y4 �
Δx
2
a b
Figure 3: Trapezoidal rule = sum of areas of trapezoids.
� �
y + y y + y y + y y + y
Total Trapezoidal Area = Δx 0 1 + 1 2 + 2 3 + ... + n−1 n
2 2 2 2
�y y �
= Δx 0 + y + y + ... + y + n
2 1 2 n−1 2
2

Lecture 24 18.01 Fall 2006
Note: The trapezoidal rule gives a more symmetric treatment of the two ends (a and b) than a
Riemann sum does — the average of left and right Riemann sums.
3. Simpson’s Rule
This approach often yields much more accurate results than the trapezoidal rule does. Here, we
match quadratics (i.e. parabolas), instead of straight or slanted lines, to the graph. This approach
requires an even number of intervals.
y
0
y
2
y
1
x₀ x₁ x₂
∆x ∆x
Figure 4: Area under a parabola.
� �
y +4y + y
Area under parabola = (base)(weighted average height) = (2Δx) 0 1 2
6
Simpson’s rule for n intervals (n must be even!)
� �
1
Area = (2Δx) [(y +4y + y )+(y +4y + y )+(y +4y + y )+ ··· +(y +4y + y )]
6 0 1 2 2 3 4 4 5 6 n−2 n−1 n
Notice the following pattern in the coefficients:
1 4 1
1 4 1
1 4 1
1 4 2 4 2 4 1
3

Lecture 24 18.01 Fall 2006
1st chunk 2nd chunk
0 1 2 3 4
Figure 5: Area given by Simpson’s rule for four intervals
Simpson’s rule:
� b Δx
f(x) dx ≈ (y +4y +2y +4y +2y + ... +4y +2y +4y + y )
3 0 1 2 3 4 n−3 n−2 n−1 n
a
The pattern of coefficients in parentheses is:
1 4 1 = sum 6
1 4 2 4 1 = sum 12
1 4 2 4 2 4 1 = sum 18
To double check – plug in f(x)=1 (n even!).
Δx Δx � �n � �n ��
(1+4+2+4+2+ ··· +2+4+1)= 1+1+4 +2 − 1 = nΔx (n even)
3 3 2 2
4

Lecture 24 18.01 Fall 2006
� 1 1
Example 1. Evaluate dx using two methods (trapezoidal and Simpson’s) of numerical
1+ x2
0
integration.
0 ∆x ∆x 1
Figure 6: Area under 1 above [0, 1].
(1+x2)
x 1/(1 + x2)
0 1
1 4
2 5
1 1
2
By the trapezoidal rule:
� � � � �� � �
1 1 1 1 4 1 1 1 1 4 1
Δx y + y + y = (1)+ + = + + =0.775
2 0 1 2 2 2 2 5 2 2 2 2 5 4
By Simpson’s rule:
� � ��
Δx 1/2 4 1
(y +4y + y )= 1+4 + =0.78333...
3 0 1 2 3 5 2
Exact answer:
� 1 1 � 1 π π
dx = tan−1 x� = tan−1 1 − tan−1 0= − 0= ≈ 0.785
0 1+ x2 � 0 4 4
Roughly speaking, the error, | Simpson’s − Exact |, has order of magnitude (Δx)4 .
5

Exam 3 Review 18.01 Fall 2006
Lecture 25: Exam 3 Review
Integration
1. Evaluate definite integrals. Substitution, first fundamental theorem of calculus (FTC 1), (and
hints?)
2. FTC 2:
d � x
f(t) dt = f(t)
dx
a
� x
If F (x)= f(t) dt, find the graph of F , estimate F , and change variables.
a
3. Riemann sums; trapezoidal and Simpson’s rules.
4. Areas, volumes.
5. Other cumulative sums: average value, probability, work, etc.
There are two types of volume problems:
1. solids of revolution
2. other (do by slices)
In these problems, there will be something you can draw in 2D, to be able to see what’s going on in
that one plane.
In solid of revolution problems, the solid is formed by revolution around the x-axis or the y-axis.
You will have to decide how to chop up the solid: into shells or disks. Put another way, you must
decide whether to integrate with dx or dy. After making that choice, the rest of the procedure is
systematically determined. For example, consider a shape rotated around the y-axis.
• Shells: height y − y , circumference 2πx, thickness dx
2 1
• Disks (washers): area πx2 (or πx2− πx2), thickness dy; integrate dy.
2 1
Work
Work = Force · Distance
We need to use an integral if the force is variable.
1

Exam 3 Review 18.01 Fall 2006
Example 1: Pendulum. See Figure 1
Consider a pendulum of length L, with mass m at angle θ. The vertical force of gravity is mg (g =
gravitational coefficient on Earth’s surface)
L
θ
mass m
mg
Figure 1: Pendulum.
In Figure 2, we find the component of gravitational force acting along the pendulum’s path
F = mg sin θ.
θ
mg
θ
Figure 2: F = mg sin θ (force tangent to path of motion).
2

Exam 3 Review 18.01 Fall 2006
Is it possible to build a perpetual motion machine? Let’s think about a simple pendulum, and
how much work gravity performs in pulling the pendulum from θ to the bottom of the pendulum’s
0
arc.
Notice that F varies. That’s why we have to use an integral for this problem.
� θ0 � θ0
W = (Force) · (Distance) = (mg sin θ)(Ldθ)
0 0
W = −Lmg cos θ
�
�
θ0
= −Lmg(cos θ − 1) = mg [L(1 − cos θ )]
� 0 0
0
In Figure 3, we see that the work performed by gravity moving the pendulum down a distance
L(1 − cos θ) is the same as if it went straight down.
θ
L
L(1-cosθ)
Figure 3: Effect of gravity on a pendulum.
In other words, the amount of work required depends only on how far down the pendulum goes.
It doesn’t matter what path it takes to get there. So, there’s no free (energy) lunch, no perpetual
motion machine.
3

