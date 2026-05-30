# MIT 18.01 Single Variable Calculus — Unit 4: Techniques of Integration and Series

> Source: MIT OpenCourseWare, http://ocw.mit.edu
> Collected: 2026-05-29
> Published: Fall 2006

MIT OpenCourseWare
http://ocw.mit.edu
18.01 Single Variable Calculus
Fall 2006
For information about citing these materials or our Terms of Use, visit: http://ocw.mit.edu/terms.

Lecture 26 18.01 Fall 2006
Lecture 26: Trigonometric Integrals and Substitution
Trigonometric Integrals
�
How do you integrate an expression like sinnx cosmxdx? (n =0, 1, 2... and m =0, 1, 2,...)
We already know that:
� �
sin xdx = − cos x + c and cos xdx = sin x + c
Method A
Suppose either n or m is odd.
�
Example 1. sin3x cos2xdx.
Our strategy is to use sin2x + cos2x =1 to rewrite our integral in the form:
� �
sin3x cos2xdx = f(cosx) sinxdx
Indeed,
� � �
sin3x cos2xdx = sin2x cos2x sin xdx = (1 − cos2x )cos2x sin xdx
Next, use the substitution
u = cos x and du = − sin xdx
Then,
� �
(1 − cos2 x) cos2 x sin xdx = (1 − u2 )u2 (−du)
� 1 1 1 1
= (−u2 + u4 )du = − u3 + u 5 + c = − cos3 u + cos5 x + c
3 5 3 5
Example 2.
� � �
cos3xdx = f(sin x) cos xdx = (1 − sin2 x) cos xdx
Again, use a substitution, namely
u = sin x and du = cos xdx
� � u3 sin3 x
cos3xdx = (1 − u 2)du = u − + c = sin x − + c
3 3
1

Lecture 26 18.01 Fall 2006
Method B
This method requires both m and n to be even. It requires double-angle formulae such as
1 + cos2x
cos2x =
2
(Recall that cos2x = cos2 x − sin2 x = cos2 x − (1 − sin2 x) = 2cos2 x − 1)
Integrating gets us
� � 1 + cos2x x sin(2x)
cos2 xdx = dx = + + c
2 2 4
We follow a similar process for integrating sin2 x.
1 − cos(2x)
sin2 x =
2
� � 1 − cos(2x) x sin(2x)
sin2xdx = dx = − + c
2 2 4
The full strategy for these types of problems is to keep applying Method B until you can apply
Method A (when one of m or n is odd).
�
Example 3. sin2 x cos2xdx.
Applying Method B twice yields
� � 1 − cos2x �� 1 + cos2x � � � 1 1 �
dx = − cos22x dx
2 2 4 4
� � 1 1 � 1 1
= − (1 + cos4x) dx = x − sin4x + c
4 8 8 32
There is a shortcut for Example 3. Because sin2x = 2 sin x cos x,
� � � 1 �2 1 � 1 − cos4x
sin2x cos2xdx = sin2x dx = dx = same as above
2 4 2
The next family of trig integrals, which we’ll start today, but will not finish is:
�
secn x tanmxdx where n =0, 1, 2,... and m =0, 1, 2,...
Remember that
sec2 x = 1+tan2 x
which we double check by writing
1 sin2 x cos2 x + sin2 x
=1+ =
cos2 x cos2 x cos3 x
� �
sec2 xdx = tan x + c sec x tan xdx = sec x + c
2

Lecture 26 18.01 Fall 2006
To calculate the integral of tan x, write
� � sin x
tan xdx = dx
cos x
Let u = cos x and du = − sin xdx, then
� � sin x � du
tan xdx = dx = − = − ln(u)+ c
cos x u
�
tan xdx = − ln(cos x)+ c
�
(We’ll figure out what sec xdx is later.)
Now, let’s see what happens when you have an even power of secant. (The case n even.)
� � �
sec4xdx = f(tanx) sec2xdx = (1 + tan2 x) sec2xdx
Make the following substitution:
u = tan x
and
du = sec2xdx
� � u3 tan3 x
sec4xdx = (1+ u2 )du = u + + c = tan x + + c
3 3
What happens when you have a odd power of tan? (The case m odd.)
� �
tan3 x sec xdx = f(sec x) d(sec x)
�
= (sec2 x − 1) sec x tan xdx
(Remember that sec2 x − 1 = tan2 x.)
Use substitution:
u = sec x
and
du = sec x tan xdx
Then,
� � u3 sec3 x
tan3 x secxdx = (u2 − 1)du = − u + c = − sec x + c
3 3
We carry out one final case: n =1,m =0
�
sec xdx = ln (tan x + sec x)+ c
3

Lecture 26 18.01 Fall 2006
We get the answer by “advanced guessing,” i.e., “knowing the answer ahead of time.”
� � sec x + tan x � � sec2 x + sec x tan x
sec xdx = sec x dx = dx
sec x + tan x tan x + sec x
Make the following substitutions:
u = tan x + sec x
and
du = (sec2 x + sec x tan x) dx
This gives
� � du
sec xdx = = ln(u)+ c = ln(tan x + sec x)+ c
u
Cases like n = 3,m = 0 or more generally n odd and m even are more complicated and will be
discussed later.
Trigonometric Substitution
Knowing how to evaluate all of these trigonometric integrals turns out to be useful for evaluating
integrals involving square roots.
�
Example 4. y = a2 − x2
a
Figure 1: Graph of the circle x2 + y2= a2.
We already know that the area of the top half of the disk is
� a � πa2
a2 − x2 dx =
2
−a
4

Lecture 26 18.01 Fall 2006
What if we want to find this area?
0 x
Figure 2: Area to be evaluated is shaded.
To do so, you need to evaluate this integral:
� t=x �
a2 − t2 dt
t=0
Let t = a sin u and dt = a cos udu. (Remember to change the limits of integration when you do a
change of variables.)
Then,
�
a2 − t2 = a2 − a2 sin2 u = a2 cos2 u; a2 − t2 = a cos u
Plugging this into the integral gives us
� x � � � u=sin−1(x/a)
a2 − t2 dt = (a cos u) a cos udu = a2 cos2 udu
0 u=0
Here’s how we calculated the new limits of integration:
t = 0 =⇒ a sin u =0 =⇒ u =0
t = x =⇒ a sin u = x =⇒ u = sin−1(x/a)
� x � � sin−1(x/a) � u sin2u ��sin−1 (x/a)
a2 − t2 dt = a2 cos2udu = a2 + �
0 0 2 4 � 0
=
a2 sin−1(x/a)
+
� a2 �
� 2sin(sin−1(x/a))cos(sin−1(x/a)) �
2 4
(Remember, sin2u = 2 sin u cos u.)
We’ll pick up from here next lecture (Lecture 28 since Lecture 27 is Exam 3).
5

Lecture 28 18.01 Fall 2006
Lecture 28: Integration by Inverse Substitution;
Completing the Square
Trigonometric Substitutions, continued
-a x a
0
Figure 1: Find area of shaded portion of semicircle.
� x �
a2 − t2dt
0
t = a sin u; dt = a cos udu
�
a2 − t2 = a2 − a2 sin2 u = a2 cos2 u =⇒ a2 − t2 = a cos u (No more square root!)
Start: x = −a ⇔ u = −π/2; Finish: x = a ⇔ u = π/2
� � � � 1 + cos(2u) � u sin(2u) �
a2 − t2 dt = a 2 cos2 udu = a2 du = a2 + + c
2 2 4
1 + cos(2u)
(Recall, cos2 u = ).
2
We want to express this in terms of x, not u. When t =0, a sin u =0, and therefore u =0.
When t = x, a sin u = x, and therefore u = sin−1(x/a).
sin(2u) 2 sin u cos u 1
= = sin u cos u
4 4 2
sin u = sin � sin−1(x/a) � = x
a
1

Lecture 28 18.01 Fall 2006
How can we find cos u = cos � sin−1(x/a) � ? Answer: use a right triangle (Figure 2).
a
x
u
√
a²-x²
p
Figure 2: sin u = x/a; cos u = a2− x2/a.
From the diagram, we see
√
a2 − x2
cos u =
a
And finally,
� x � � u 1 � � sin−1(x/a) 1 � x � √ a2 − x2 �
a2 − t2 dt = a2 + sin u cos u − 0= a 2 +
4 2 2 2 a a
0
� x � a2 x 1 �
a2 − t2 dt = sin−1( )+ x a2 − x2
2 a 2
0
When the answer is this complicated, the route to getting there has to be rather complicated.
There’s no way to avoid the complexity.
1
Let’s double-check this answer. The area of the upper shaded sector in Figure 3 is a2 u. The
√ √2
area of the lower shaded region, which is a triangle of height a2 − x2 and base x, is 1 x a2 − x2.
2
2

Lecture 28 18.01 Fall 2006
u
x
0
Figure 3: Area divided into a sector and a triangle.
Here is a list of integrals that can be computed using a trig substitution and a trig identity.
integral substitution trig identity
� dx
√ x = tan u tan2 u +1 = sec2 u
x2 +1
� dx
√ x = sec u sec2 u − 1 = tan2 u
x2 − 1
� dx
√ x = sin u 1 − sin2 u = cos2 u
1 − x2
Let’s extend this further. How can we evaluate an integral like this?
� dx
√
x2 +4x
When you have a linear and a quadratic term under the square root, complete the square.
x 2 +4x =(something)2 ± constant
In this case,
(x + 2)2 = x2 +4x +4 =⇒ x 2 +4x =(x + 2)2 − 4
Now, we make a substitution.
v = x +2 and dv = dx
Plugging these in gives us
� dx � dv
= √
�
(x + 2)2 − 4 v2 − 4
Now, let
v = 2 sec u and dv = 2 sec u tan u
� dv � 2sec u tan udu �
√ = = sec udu
v2 − 4 2 tan u
3

Lecture 28 18.01 Fall 2006
Remember that
�
sec udu = ln(sec u + tan u)+ c
Finally, rewrite everything in terms of x.
2
v = 2 sec u ⇔ cos u =
v
Set up a right triangle as in Figure 4. Express tan u in terms of v.
v
√v²-4
u
2
Figure 4: sec u = v/2 or cos u =2/v.
Just from looking at the triangle, we can read off
√
v v2 − 4
sec u = and tan u =
2 2
� √ �
� v v2 − 4
2sec udu = ln + + c
2 2
�
= ln(v + v2 − 4) − ln2 + c
We can combine those last two terms into another constant, c˜.
� dx �
√ = ln(x +2+ x2 +4x)+c˜
x2 +4x
Here’s a teaser for next time. In the next lecture, we’ll integrate all rational functions. By
“rational functions,” we mean functions that are the ratios of polynomials:
P (x)
Q(x)
It’s easy to evaluate an expression like this:
� � 1 3 �
+ dx = ln |x − 1| + 3ln |x +2| + c
x − 1 x +2
4

Lecture 28 18.01 Fall 2006
If we write it a bit differently, however, it becomes much harder to integrate:
1 3 x + 2 + 3(x − 1) 4x − 1
+ = =
x − 1 x +2 (x − 1)(x + 2) x2 + x − 2
� 4x − 1
= ???
x2 + x − 2
How can we reorganize what to do starting from (4x − 1)/(x2 + x − 2)? Next time, we’ll see how.
It involves some algebra.
5

Lecture 29 18.01 Fall 2006
Lecture 29: Partial Fractions
We continue the discussion we started last lecture about integrating rational functions. We
defined a rational function as the ratio of two polynomials:
P (x)
Q(x)
We looked at the example
� � 1 3 �
+ dx = ln |x − 1| + 3ln |x +2| + c
x − 1 x +2
That same problem can be disguised:
1 3 (x + 2) + 3(x − 1) 4x − 1
+ = =
x − 1 x +2 (x − 1)(x + 2) x2 + x − 2
which leaves us to integrate this:
� 4x − 1
dx = ???
x2 + x − 2
P (x)
Goal: we want to figure out a systematic way to split into simpler pieces.
Q(x)
First, we factor the denominator Q(x).
4x − 1 4x − 1 A B
= = +
x2 + x − 2 (x − 1)(x + 2) x − 1 x +2
There’s a slow way to find A and B. You can clear the denominator by multiplying through by
(x − 1)(x + 2):
(4x − 1) = A(x + 2) + B(x − 1)
From this, you find
4= A + B and − 1=2A − B
You can then solve these simultaneous linear equations for A and B. This approach can take a very
long time if you’re working with 3, 4, or more variables.
There’s a faster way, which we call the “cover-up method”. Multiply both sides by (x − 1):
4x − 1 B
= A + (x − 1)
x +2 x + 2
Set x =1 to make the B term drop out:
4 − 1
= A
1+2
A =1
1

Lecture 29 18.01 Fall 2006
The fastest way is to do this in your head or physically cover up the struck-through terms. For
instance, to evaluate B:
4x − 1 A� B
(x − 1)�(x� + �� 2) = �x � − 1 + �(x� + � � 2)
Implicitly, we are multiplying by (x + 2) and setting x = −2. This gives us
4(−2) − 1
= B =⇒ B =3
−2 − 1
What we’ve described so far works when Q(x) factors completely into distinct factors and the
degree of P is less than the degree of Q.
If the factors of Q repeat, we use a slightly different approach. For example:
x2 +2 A B C
= + +
(x − 1)2(x + 2) x − 1 (x − 1)2 x +2
Use the cover-up method on the highest degree term in (x − 1).
x2 +1 12 +2
= B +[stuff](x − 1)2 =⇒ = B =⇒ B =1
x +2 1+2
Implicitly, we multiplied by (x − 1)2, then took the limit as x → 1.
C can also be evaluated by the cover-up method. Set x = −2 to get
x2 +2 2 (−2)2 +2 2
= C +[stuff](x +2) =⇒ = C =⇒ C =
(x − 1) (−2 − 1)2 3
This yields
x2 +2 A 1 2/3
= + +
(x − 1)2(x + 2) x − 1 (x − 1)2 x +2
Cover-up can’t be used to evaluate A. Instead, plug in an easy value of x: x =0.
2 A 1 1 1
= +1+ =⇒ 1=1+ − A =⇒ A =
(−1)2(2) −1 3 3 3
Now we have a complete answer:
x2 +2 1 1 2
= + +
(x − 1)2(x + 2) 3(x − 1) (x − 1)2 3(x + 2)
Not all polynomials factor completely (without resorting to using complex numbers). For exam­
ple:
1 A B x + C
= 1 + 1 1
(x2 + 1)(x − 1) x − 1 x2 +1
We find A , as usual, by the cover-up method.
1
1 1
= A =⇒ A =
12 +1 1 1 2
2

Lecture 29 18.01 Fall 2006
Now, we have
1 1/2 B x + C
= + 1 1
(x2 + 1)(x − 1) x − 1 x2 +1
Plug in x =0.
1 1 C 1
= − + 1 =⇒ C = −
1(−1) 2 1 1 2
Now, plug in any value other than x =0, 1. For example, let’s use x = −1.
1 1/2 B (−1) − 1/2 B − 1/2 1
= + 1 =⇒ 0= − 1 =⇒ B = −
2(−2) −2 2 2 1 2
Alternatively, you can multiply out to clear the denominators (not done here).
Let’s try to integrate this function, now.
� dx 1 � dx 1 � xdx 1 � dx
= − −
(x2 + 1)(x − 1) 2 x − 1 2 x2 +1 2 x2 +1
1 1 1
= ln |x − 1|− ln | x 2 +1 |− tan−1 x + c
2 4 2
What if we’re faced with something that looks like this?
� dx
(x − 1)10
This is actually quite simple to integrate:
� dx 1
= − (x − 1)−9 + c
(x − 1)10 9
What about this?
� dx
(x2 + 1)10
Here, we would use trig substitution:
x = tan u and dx = sec2 udu
and the trig identity
tan2 u +1 = sec2 u
to get
� sec2 udu �
= cos18 udu
(sec2 u)10
From here, we can evaluate this integral using the methods we introduced two lectures ago.
3

Lecture 30 18.01 Fall 2006
Lecture 30: Integration by Parts, Reduction
Formulae
Integration by Parts
Remember the product rule:
(uv)� = u�v + uv�
We can rewrite that as
uv� =(uv)� − u�v
Integrate this to get the formula for integration by parts:
� �
uv� dx = uv − u�v dx
�
Example 1. tan−1 xdx.
At first, it’s not clear how integration by parts helps. Write
� � �
tan−1 xdx = tan−1 x(1 · dx)= uv� dx
with
u = tan−1 x and v� =1.
Therefore,
1
v = x and u� =
1+ x2
Plug all of these into the formula for integration by parts to get:
� � � 1
tan−1 xdx = uv� dx = (tan−1 x)x − (x)dx
1+ x2
1
= x tan−1 x − ln |1+ x 2| + c
2
Alternative Approach to Integration by Parts
As above, the product rule:
(uv)� = u�v + uv�
can be rewritten as
uv� =(uv)� − u�v
This time, let’s take the definite integral:
� b � b � b
uv� dx = (uv)� dx − u�v dx
a a a
1

Lecture 30 18.01 Fall 2006
By the fundamental theorem of calculus, we can say
� b �b � b
uv� dx = uv� − u�v dx
�
a a a
Another notation in the indefinite case is
� �
udv = uv − v du
This is the same because
dv = v� dx =⇒ uv� dx = udv and du = u� dx =⇒ u�v dx = vu� dx = v du
�
Example 2. (ln x)dx
1
u = ln x; du = dx and dv = dx; v = x
x
� � � 1 � �
(ln x)dx = x ln x − x dx = x ln x − dx = x ln x − x + c
x
We can also use “advanced guessing” to solve this problem. We know that the derivative of
something equals ln x:
d
(??) = ln x
dx
Let’s try
d 1
(x ln x) = ln x + x · = ln x +1
dx x
That’s almost it, but not quite. Let’s repair this guess to get:
d
(x ln x − x) = ln x +1 − 1 = ln x
dx
Reduction Formulas (Recurrence Formulas)
�
Example 3. (ln x)n dx
Let’s try:
� �
1
u = (ln x)n =⇒ u� = n(ln x)n−1
x
v� = dx; v = x
Plugging these into the formula for integration by parts gives us:
� � � 1����
1
(ln x)ndx = x(ln x)n − n(ln x)n−1 x � dx
� x
Keeprepeatingintegrationbypartstogetthefullformula: n →(n − 1) →(n − 2) →(n − 3) → etc
�
Example 4. xn e x dx Let’s try:
u = xn =⇒ u� = nxn −1; v� = ex =⇒ v = ex
2

Lecture 30 18.01 Fall 2006
Putting these into the integration by parts formula gives us:
� �
xn ex dx = xnex − nxn −1 e x dx
Repeat, going from n → (n − 1) → (n − 2) → etc.
Bad news: If you change the integrals just a little bit, they become impossible to evaluate:
�
� tan−1 x �2 dx = impossible
� ex
dx = also impossible
x
Good news: When you can’t evaluate an integral, then
� 2 ex
dx
x
1
is an answer, not a question. This is the solution– you don’t have to integrate it!
The most important thing is setting up the integral! (Once you’ve done that, you can always
evaluate it numerically on a computer.) So, why bother to evaluate integrals by hand, then? Because
you often get families of related integrals, such as
� ∞ ex
F (a)= dx
xa
1
where you want to find how the answer depends on, say, a.
3

Lecture 30 18.01 Fall 2006
Arc Length
This is very useful to know for 18.02 (multi-variable calculus).
y
ds
y=f(x) dy
dx
x
Figure 1: InfinitesimalArcLength ds
ds
dy
dx
Figure 2: Zoom in on Figure 1 to see an approximate right triangle.
In Figures 1 and 2, s denotes arc length and ds = the infinitesmal of arc length.
�
ds = � (dx)2 +(dy)2 = 1+(dy/dx)2dx
Integrating with respect to ds finds the length of a curve between two points (see Figure 3).
To find the length of the curve between P and P , evaluate:
0 1
� P1
ds
P0
4

Lecture 30 18.01 Fall 2006
P₁
P₀
a b
Figure 3: Findlengthofcurvebetween P0 and P1.
We want to integrate with respect to x, not s, so we do the same algebra as above to find ds in
terms of dx.
(ds)2 (dx)2 (dy)2 � dy �2
= + =1+
(dx)2 (dx)2 (dx)2 dx
Therefore,
�
� P1 � b � dy �2
ds = 1+ dx
dx
P0 a
Example 5: The Circle. x2 + y 2 =1 (see Figure 4).
Figure 4: ThecircleinExample1.
5

Lecture 30 18.01 Fall 2006
We want to find the length of the arc in Figure 5:
a
Figure 5: Arclengthtobeevaluated.
�
y = 1 − x2
� �
dy −2x 1 −x
= √ = √
dx 1 − x2 2 1 − x2
�
�
−x
�2
ds = 1+ √ dx
1 − x2
� −x �2 x2 1 −x2 + x2 1
1+ √ =1+ = =
1 − x2 1 − x2 1 − x2 1 − x2
�
1
ds = dx
1 − x2
� a dx ⏐a
s = √ = sin−1 x⏐ = sin−1 a − sin−1 0 = sin−1 a
0 1 − x2 ⏐ 0
sin s = a
This is illustrated in Figure 6.
6

Lecture 30 18.01 Fall 2006
s
a
1
a
1
Figure 6: s = angleinradians.
Parametric Equations
Example 6.
x = a cos t
y = a sin t
Ask yourself: what’s constant? What’s varying? Here, t is variable and a is constant.
Is there a relationship between x and y? Yes:
x 2 + y 2 = a2 cos2 t + a 2 sin2 t = a2
Extra information (besides the circle):
At t =0,
x = a cos0 = a and y = a sin0 = 0
π
At t = ,
2
π π
x = a cos =0 and y = a sin = a
2 2
Thus, for 0 ≤ t ≤ π/2, a quarter circle is traced counter-clockwise (Figure 7).
7

Lecture 30 18.01 Fall 2006
t=π/2
(0,a)
(a,0)
t=0
Figure 7: Example6. x = a cos t, y = a sin t; theparticleismovingcounterclockwise.
Example 7: The Ellipse See Figure 8.
x = 2 sin t; y = cos t
x2
+ y 2 = 1( =⇒ (2sin t)2/4 + (cos t)2 = sin2t + cos2t = 1)
4
t=0
(0,1)
(2,0)
t=π/2
Figure 8: Ellipse: x = 2 sin t, y = cos t (tracedclockwise).
Arclength ds for Example 6.
dx = −a sin t dt, dy = a cos tdt
� � �
ds = (dx)2 +(dy)2 = (−a sin tdt)2 +(a cos tdt)2 = (a sin t)2 +(a cos t)2 dt = adt
8

Lecture 31 18.01 Fall 2006
Lecture 31: Parametric Equations, Arclength,
Surface Area
Arclength, continued
Example 1. Consider this parametric equation:
x = t2 y = t3 for 0 ≤ t ≤ 1
x 3 =(t2)3 = t6; y 2 =(t3)2 = t6 =⇒ x 3 = y 2 =⇒ y = x2 /3 0 ≤ x ≤ 1
ds
dy
ds
dy
dx
dx
Figure 1: InfinitesimalArclength.
(ds)2 =(dx)2 +(dy)2
(ds)2 = (2tdt)2 +(3t2 dt)2 = (4t2 +9t4)(dt)2
� �� � � �� �
(dx)2 (dy)2
� t=1 � 1 � � 1 �
Length = ds = 4t2 +9t4dt = t 4+9t2dt
t=0 0 0
(4+9t2)3/2 �1 1
= � = (133/2 − 43/2)
27 � 0 27
Even if you can’t evaluate the integral analytically, you can always use numerical methods.
1

Lecture 31 18.01 Fall 2006
Surface Area (surfaces of revolution)
y
ds
y
x
a b
Figure 2: Calculatingsurfacearea
ds (the infinitesimal curve length in Figure 2) is revolved a distance 2πy. The surface area of the
thin strip of width ds is 2πy ds.
Example 2. Revolve Example 1 (x = t2,y = t3 , 0 ≤ t ≤ 1) around the x-axis. Refer to Figure 3.
y
x
Figure 3: Curvedsurfaceofatrumpet.
2

Lecture 31 18.01 Fall 2006
� � 1 2π t3 t � 4+9t2 dt � 1 �
Area = 2πy ds =
0 ���� � �� �
=2π t4 4+9t2 dt
y ds 0
Now, we discuss the method used to evaluate
�
t4(4 + 9t2)1/2dt
We’re going to ignore the factor of 2π. You can reinsert it once you’re done evaluating the integral.
We use the trigonometric substitution
2 2
t = tan u; dt = sec2 udu; tan2 u +1 = sec2 u
3 3
Putting all of this together gives us:
� � � 2 �4 � � 4 ��1/2 � 2 �
t4(4 + 9t2)1/2 dt = tan u 4+9 tan2 u sec2 udu
3 9 3
� 2 �5 �
= tan4 u(2sec u)(sec2 udu)
3
This is a tan − sec integral. It’s doable, but it will take a long time for you to work the whole thing
out. We’re going to stop evaluating it here.
Example 3 Let’s use what we’ve learned to find the surface area of the unit sphere (see Figure 4).
y
rotate the curve
by 2π radians
. .
b x
a
Figure 4: Sliceofsphericalsurface(orangepeel,only,nottheinsides).
3

Lecture 31 18.01 Fall 2006
For the top half of the sphere,
�
y = 1 − x2
We want to find the area of the spherical slice between x = a and x = b. A spherical slice has area
� x=b
A = 2πy ds
x=a
From last time,
dx
ds = √
1 − x2
Plugging that in yields a remarkably simple formula for A:
� b � dx � b
A = 2π 1 − x2 √ = 2π dx
1 − x2
a a
=2π(b − a)
Special Cases
For a whole sphere, a = −1, and b =1.
2π(1 − (−1)) = 4π
is the surface area of a unit sphere.
For a half sphere, a =0 and b =1.
2π(1 − 0) = 2π
4

Lecture 32 18.01 Fall 2006
Lecture 32: Polar Co-ordinates, Area in Polar
Co-ordinates
Polar Coordinates
r
θ
Figure 1: PolarCo-ordinates.
In polar coordinates, we specify an object’s position in terms of its distance r from the origin
and the angle θ that the ray from the origin to the point makes with respect to the x-axis.
Example 1. What are the polar coordinates for the point specified by (1, −1) in rectangular
coordinates?
r
(1,-1)
Figure 2: RectangularCo-ordinatestoPolarCo-ordinates.
√
�
r = 12 +(−1)2 = 2
π
θ = −
4
Inmost cases,we usetheconventionthat r ≥ 0 and 0 ≤ θ ≤ 2π. Butanother commonconvention
is to say r ≥ 0 and −π ≤ θ ≤ π. All values of θ and even negative values of r can be used.
1

Lecture 32 18.01 Fall 2006
r
y
θ
x
Figure 3: RectangularCo-ordinatestoPolarCo-ordinates.
Regardless of whether we allow positive or negative values of r or θ, what is always true is:
x = r cos θ and y = r sin θ
√ 3π
For instance, x =1, y = −1 can be represented by r = − 2, θ = :
4
√ 3π √ 3π
1= x = − 2 cos and − 1= y = − 2 sin
4 4
Example 2. Consider a circle of radius a with its center at x = a, y = 0. We want to find an
equation that relates r to θ.
(a,0)
Figure 4: Circleofradius a withcenterat x = a,y =0.
2

Lecture 32 18.01 Fall 2006
We know the equation for the circle in rectangular coordinates is
(x − a)2 + y 2 = a2
Start by plugging in:
x = r cos θ and y = r sin θ
This gives us
(r cos θ − a)2 +(r sin θ)2 = a2
r 2cos2θ − 2arcosθ + a2 + r 2sin2θ = a2
r 2 − 2ar cos θ =0
r =2a cos θ
π π
Therangeof 0 ≤ θ ≤ tracesoutthetophalfofthecircle,while − ≤ θ ≤ 0 tracesoutthebottom
2 2
half. Let’s graph this.
y
θ = π/4
r
θ
x
(a,0) θ = 0
Figure 5: r =2a cos θ, −π/2 ≤ θ ≤ π/2.
At θ =0, r =2a =⇒ x =2a, y =0
π π √
At θ = , r =2a cos = a 2
4 4
−π π
The main issue is finding the range of θ tracing the circle once. In this case, <θ < .
2 2
π
θ = − (down)
2
π
θ = (up)
2
π 3π
Weird range (avoid this one): <θ < . When θ = π, r =2a cos π =2a(−1) = −2a. The
2 2
π 3π
radius points “backwards”. In the range <θ < , the same circle is traced out a second time.
2 2
3

Lecture 32 18.01 Fall 2006
r=f(θ)
Figure 6: Usingpolarco-ordinatestofindareaofagenericfunction.
Area in Polar Coordinates
Since radius is a function of angle (r = f(θ)), we will integrate with respect to θ. The question
is: what, exactly, should we integrate?
� θ2
?? dθ
θ1
Let’s look at a very small slice of this region:
rdθ
dθ
r
Figure 7: Approximatesliceofareainpolarcoordinates.
This infinitesimal slice is approximately a right triangle. To find its area, we take:
1 1
Area of slice ≈ (base)(height)= r(r dθ)
2 2
So,
� θ2 1
Total Area = r 2 dθ
2
θ1
4

Lecture 32 18.01 Fall 2006
π π
Example 3. r =2a cos θ, and − <θ < (the circle in Figure 5).
2 2
� π/2 1 � π/2
A = area = (2a cos θ)2 dθ =2a 2 cos2θ dθ
2
−π/2 −π/2
1 1
Because cos2 θ = + cos2θ, we can rewrite this as
2 2
� π/2 � π/2 � π/2
A = area = (1+cos2θ) dθ = a2 dθ + a2 cos2θ dθ
−π/2 −π/2 −π/2
= πa2 + 1
2
sin2θ
�
� � π
−
/
π
2
/ 2
= πa2 + 1
2�
[si�n π� −� s � in( � − � π) �� ] 0
A = area = πa2
Example 4: Circle centered at the Origin.
r=a
Figure 8: Example 4: Circle centered at the origin
x = r cos θ; y = r sin θ
x2 + y 2 = r 2 cos2 θ + r 2 sin2 θ = r 2
The circle is x2 + y2 = a2, so r = a and
x = a cos θ; y = a sin θ
� 2π 1 1
A = a2 dθ = a 2 · 2π = πa2 .
2 2
0
5

Lecture 32 18.01 Fall 2006
Example 5: A Ray. In this case, θ = b.
θ=b
Figure 9: Example 5: The ray θ = b, 0 ≤ r< ∞.
The range of r is 0 ≤ r < ∞; x = r cos b; y = r sin b.
Example 6: Finding the Polar Formula, based on the Cartesian Formula
y
1
1/sin θ
θ x
Figure 10: Example 6: Cartesian Form to Polar Form
Consider, in cartesian coordinates, the line y = 1. To find the polar coordinate equation, plug
in y = r sin θ and x = r cos θ and solve for r.
1
r sin θ =1 =⇒ r = with 0 <θ <π
sin θ
6

Lecture 32 18.01 Fall 2006
Example 7: Going back to (x,y) coordinates from r = f(θ).
Start with
1
r = .
1+ 1 sin θ
2
Hence,
r
r + sin θ =1
2
�
Plug in r = x2 + y2:
� y
x2 + y2 + =1
2
� y � y �2 y2
x2 + y2 =1 − =⇒ x 2 + y 2 = 1 − =1 − y +
2 2 4
Finally,
3y2
x 2 + + y =1
4
This is an equation for an ellipse, with the origin at one focus.
Useful conversion formulas:
� � y �
r = x2 + y2 and θ = tan−1
x
Example 8: A Rose r = cos(2θ)
The graph looks a bit like a flower:
r<0 π/4
r>0
1
r>0
r<0 -π/4
Figure 11: Example 8: Rose
For the first “petal”
π π
− <θ <
4 4
Note: Next lecture is Lecture 34 as Lecture 33 is Exam 4.
7

Lecture 32: Exam 4 Review 18.01 Fall 2006
Exam 4 Review
1. Trig substitution and trig integrals.
2. Partial fractions.
3. Integration by parts.
4. Arc length and surface area of revolution
5. Polar coordinates
6. Area in polar coordinates.
Questions from the Students
• Q: What do we need to know about parametric equations?
• A: Just keep this formula in mind:
�
�
dx
�2 �
dy
�2
ds = +
dt dt
Example: You’re given
x(t)= t4
and
y(t)=1+ t
Find s (length).
�
ds = (4t3)2 + (1)2dt
Then, integrate with respect to t.
• Q: Can you quickly review how to do partial fractions?
• A: When finding partial fractions, first check whether the degree of the numerator is greater
than or equal to the degree of the denominator. If so, you first need to do algebraic long-
division. If not, then you can split into partial fractions.
Example.
x2 + x +1
(x − 1)2(x + 2)
We already know the form of the solution:
x2 + x +1 A B C
= + +
(x − 1)2(x + 2) x − 1 (x − 1)2 x +2
There are two coefficients that are easy to find: B and C. We can find these by the cover-up
method.
12 +1+1 3
B = = (x → 1)
1+2 3
1

Lecture 32: Exam 4 Review 18.01 Fall 2006
To find C,
(−2)2 − 2+1 1
C = = (x →−2)
(−2 − 1)2 3
To find A, one method is to plug in the easiest value of x other than the ones we already used
(x =1, −2). Usually, we use x =0.
1 A 1 1/3
= + +
(−1)2(2) −1 (−1)2 2
and then solve to find A.
The Review Sheet handed out during lecture follows on the next page.
2

Lecture 32: Exam 4 Review 18.01 Fall 2006
Exam 4 Review Handout
1. Integrate by trigonometric substitution; evaluate the trigonometric integral and work
backwards to the original variable by evaluating trig(trig−1) using a right triangle:
a) a2 − x2 use x = a sin u, dx = a cos udu.
b) a2 + x2 use x = a tan u, dx = a sec2 udu
c) x2 − a2 use x = a sec u, dx = a sec u tan udu
2. Integrate rational functions P/Q (ratio of polynomials) by the method of partial fractions:
If the degree of P is less than the degree of Q, then factor Q completely into linear and quadratic
factors, and write P/Q as a sum of simpler terms. For example,
3x2 +1 A B B Cx + D
= + 1 + 2 +
(x − 1)(x + 2)2(x2 + 9) x − 1 (x +2) (x + 2)2 x2 +9
Terms such as D/(x2 + 9) can be integrated using the trigonometric substitution x = 3 tan u.
This method can be used to evaluate the integral of any rational function. In practice, the
hard part turns out to be factoring the denominator! In recitation you encountered two other steps
required to cover every case systematically, namely, completing the square1 and long division.2
3. Integration by parts:
� b
�
�
b
� b
uv�dx = uv � − u�vdx
�
a � a
a
This is used when u�v is simpler than uv�. (This is often the case if u� is simpler than u.)
�
4. Arclength: ds = dx2 + dy2. Depending on whether you want to integrate with respect to
x, t or y this is written
� � �
ds = 1+(dy/dx)2 dx; ds = (dx/dt)2 +(dy/dt)2 dt; ds = (dx/dy)2 +1 dy
5. Surface area for a surface of revolution:
�
a) around the x-axis: 2πyds =2πy 1+(dy/dx)2 dx (requires a formula for y = y(x))
�
b) around the y-axis: 2πxds =2πx (dx/dy)2 +1 dy (requires a formula for x = x(y))
�
6. Polar coordinates: x = r cos θ, y = r sin θ (or, more rarely, r = x2 + y2, θ = tan−1(y/x))
a) Find the polar equation for a curve from its equation in (x,y) variables by substitution.
b)Sketchcurvesgiven inpolarcoordinatesandunderstandtherangeofthe variable θ (often
in preparation for integration).
7. Area in polar coordinates:
� θ2 1
r 2dθ
2
θ1
(Pay attention to the range of θ to be sure that you are not double-counting regions or missing
them.)
1For example, we rewrite the denominator x2 +4x +13 = (x + 2)2 +9= u2 + a2 with u = x +2 and a =3.
2Long division is used when the degree of P is greater than or equal to the degree of Q. It expresses P (x)/Q(x)=
P1(x)+ R(x)/Q(x) with P1 a quotient polynomial (easy to integrate) and R a remainder. The key point is that the
remainder R has degree less than Q, so R/Q can be split into partial fractions.
3

Lecture 32: Exam 4 Review 18.01 Fall 2006
The following formulas will be printed with Exam 4
sin2 x + cos2 x = 1; sec2 x = tan2 x +1
1 1 1 1
sin2 x = − cos2x; cos2 x = + cos2x
2 2 2 2
cos2x = cos2 x − sin2 x; sin 2x = 2 sin x cos x
d d d 1 d 1
tan x = sec2 x; sec x = sec x tan x; tan−1 x = ; sin−1 x = √
dx dx dx 1+ x2 dx 1 − x2
� �
tan xdx = − ln(cos x)+ c; sec xdx = ln(sec x + tan x)+ c
See the next page for a review on integration of rational functions.
4

Lecture 32: Exam 4 Review 18.01 Fall 2006
Postscript: Systematic integration of rational functions
For a general rational function P/Q, the first step is to express P/Q as the sum of a polynomial
and a ratio in which the numerator has smaller degree than the denominator.
For example,
x3 3x − 2
= x +2+
x2 − 2x +1 x2 − 2x +1
(To carry out this long division, do not factor the denominator Q(x) = x2 − 2x +1, just leave it
alone.) The quotient x +2 is a polynomial and is easy to integrate. The remainder term
3x − 2
(x − 1)2
has a numerator 3x − 2 of degree 1 which is less than the degree 2 of the denominator (x − 1)2 .
Therefore there is a partial fraction decomposition. In fact,
3x − 2 (3x − 3)+1 3 1
= = +
(x − 1)2 (x − 1)2 x − 1 (x − 1)2
In general, if P has degree n and Q has degree m, then long division gives
P (x) R(x)
= P (x)+
Q(x) 1 Q(x)
in which P , the quotient in the long division, has degree n − m and R, the remainder in the long
1
division, has degree at most m − 1.
Evaluation of the “simple” pieces
The integral
� dx −1
= (x − a)1−n + c
(x − a)n n − 1
if n =� 1 and ln |x − a| + c if n =1. On the other hand the terms
� xdx � dx
and
(Ax2 + Bx + C)n (Ax2 + Bx + C)n
are handled by first completing the square:
� B2 �
Ax2 + Bx + C = A(x − B/2A)2 + C −
4A
√
Using the variable u = A(x − B/2A) yields combinations of integrals of the form
� udu � du
and
(u2 + k2)n (u2 + k2)n
The first integral is handled by the substitution w = u2 + k2 , dw =2udu. The second integral can
be worked out using the trigonometric substitution u = k tan θ du = k sec2 θdθ. This then leads to
sec-tan integrals, and the actual computation for large values of n are long.
There are also other cases that we will not cover systematically. Examples are below:
1. If Q(x)=(x − a)m(x − b)n, then the expression is
A A A B B B
1 + 2 +··· + m + 1 + 2 +··· + n
x − a (x − a)2 (x − a)m x − b (x − b)2 (x − b)n
5

Lecture 32: Exam 4 Review 18.01 Fall 2006
2. If there are quadratic factors like (Ax2 + Bx + C)p, one gets terms
a x + b a x + b x a x + b
1 1 + 2 2 +··· + p p
Ax2 + Bx + C (Ax2 + Bx + C)2 (Ax2 + Bx + C)p
for each such factor. (To integrate these quadratic pieces complete the square and make a
trigonometric substitution.)
6

Lecture 34 18.01 Fall 2006
Lecture 34: Indeterminate Forms - L’Hôpital’s Rule
L’Hôpital’s Rule
(Two correct spellings: “L’Hôpital” and “L’Hospital”)
Sometimes, we run into indeterminate forms. These are things like
0
0
and
∞
∞
For instance, how do you deal with the following?
x3 − 1 0
lim = ??
x→1 x2 − 1 0
Example 0. One way of dealing with this is to use algebra to simplify things:
x3 − 1 (x − 1)(x2 + x + 1) x2 + x +1 3
lim = lim = lim =
x→1 x2 − 1 x→1 (x − 1)(x + 1) x→1 x +1 2
In general, when f(a)= g(a)=0,
f(x) f(x) − f(a)
lim
f(x) x − a x→a x − a f�(a)
lim = lim = =
x→a g(x) x→a g(x) g(x) − g(a) g�(a)
lim
x − a x→a x − a
This is the easy version of L’Hôpital’s rule:
f(x) f�(a)
lim =
x→a g(x) g�(a)
Note: this only works when g�(a)=� 0!
In example 0,
f(x)= x 3 = 1; g(x)= x 2 − 1
f�(x)=3x 2; g�(x)=2x =⇒ f�(1) = 3; g�(1) = 2
The limit is f�(1)/g�(1) = 3/2. Now, let’s go on to the full L’Hôpital rule.
1

Lecture 34 18.01 Fall 2006
Example 1. Apply L’Hôpital’s rule (a.k.a. “L’Hop”) to
x15 − 1
lim
x→1 x3 − 1
to get
x15 − 1 15x14 15
lim = lim = =5
x→1 x3 − 1 x→1 3x2 3
Let’s compare this with the answer we’d get if we used linear approximation techniques, instead of
L’Hôpital’s rule:
x1 5 − 1 ≈ 15(x − 1)
(Here, f(x)= x15 − 1,a =1,f(a)= b =0,m = f�(1) = 15, and f(x) ≈ m(x − a)+ b.)
Similarly,
x 3 − 1 ≈ 3(x − 1)
Therefore,
x15 − 1 15(x − 1)
≈ =5
x3 − 1 3(x − 1)
Example 2. Apply L’Hop to
sin3x
lim
x→0 x
to get
3cos3x
lim =3
x→0 1
This is the same as
d � �
sin(3x) � = 3 cos(3x) � =3
dx � x=0 � x=0
Example 3.
sin x − cos x cos x + sin x 1 1 √
lim = lim = √ + √ = 2
x→ π x − π x→ π 1 2 2
4 4 4
f(x) = sin x − cos x, f�(x) = cos x + sin x
�π � √
f� = 2
4
Δy 0
Remark: Derivatives lim are always a type of limit.
Δx→0 Δx 0
cos x − 1
Example 4. lim .
x→0 x
Use L’Hôpital’s rule to evaluate the limit:
cos x − 1 − sin x
lim = lim =0
x→0 x x→0 x
2

Lecture 34 18.01 Fall 2006
cos x − 1
Example 5. lim .
x→0 x2
cos x − 1 cos x − 1 − sin x − cos x 1
lim = lim = lim = lim = −
x→0 x2 x→0 x2 x→0 2x x→0 2 2
Justtocheck,let’scomparethatanswertotheonewewouldgetifweusedquadraticapproximation
techniques. Remember that:
1
cos x ≈ 1 − x 2 (x ≈ 0)
2
1 1
1 − x 2 − 1 (− )x2
cos x − 1 2 2 1
≈ = = −
x2 x2 x2 2
sin x
Example 6. lim .
x→0 x2
sin x cos x
lim = lim By L’Hôpital’s rule
x→0 x2 x→0 2x
If we apply L’Hôpital again, we get
sin x
lim − =0
x→0 2
But this doesn’t agree with what we get from taking the linear approximation:
sin x x 1
≈ = →∞ as x → 0+
x2 x2 x
We can clear up this seeming paradox by noting that
cos x 1
lim =
x→0 2x 0
0
The limit is not of the form , which means L’Hôpital’s rule cannot be used. The point is: look
0
before you L’Hôp!
More “interesting” cases that work.
∞
It is also okay to use L’Hôpital’s rule on limits of the form , or if x → ∞, or x → −∞. Let’s
∞
apply this to rates of growth. Which function goes to ∞ faster: x, e ax, or ln x?
Example 7. For a> 0,
eax aeax
lim = lim =+∞
x→∞ x x→∞ 1
So ea x grows faster than x (for a> 0).
Example 8.
eax aeax c2eax a10eax
lim = by L’Hôpital = lim = lim = ··· = lim = ∞
x→∞ x10 x→∞ 10x9 x→∞ 10 · 9x8 x→∞ 10!
3

Lecture 34 18.01 Fall 2006
You can apply L’Hôpital’s rule ten times. There’s a better way, though:
� eax �1/10 eax/10
=
x10 x
eax � eax/10 �10
lim = lim = ∞10 = ∞
x→∞ x10 x→∞ x
Example 9.
ln x 1/x
lim = lim = lim 3x−1/3 =0
x→∞ x1/3 x→∞ 1/3x−2/3 x→∞
Combining the preceding examples, ln x � x 1/3 � x � x 10 � e ax (x →∞,a > 0)
0 ∞
L’Hôpital’s rule applies to and . But, we sometimes face other indeterminate limits, such
0 ∞
as 1∞, 00, and 0 ·∞. Use algebra, exponentials, and logarithms to put these in L’Hôpital form.
Example 10. lim xx for x> 0.
x→0
Because the exponent is a variable, use base e:
lim xx = lim ex ln x
x→0 x→0
First, we need to evaluate the limit of the exponent
lim x ln x
x→0
0 ∞
This limit has the form 0 ·∞. We want to put it in the form or .
0 ∞
0
Let’s try to put it into the form:
0
x
1/ ln x
1
We don’t know how to find lim , though, so that approach isn’t helpful.
x→0 ln x
∞
Instead, let’s try to put it into the form:
∞
ln x
1/x
Using L’Hôpital’s rule, we find
ln x 1/x
lim x ln x = lim = lim = lim(−x)=0
x→0 x→0 1/x x→0 −1/x2 x→0
Therefore,
lim(x ln x)
lim xx = lim ex ln x = e x→0 = e0 =1
x→0 x→0
4

Lecture 35 18.01 Fall 2006
Lecture 35: Improper Integrals
Definition.
An improper integral, defined by
� ∞ � M
f(x)dx = lim f(x)dx
a M→∞ a
is said to converge if the limit exists (diverges if the limit does not exist).
� ∞
Example 1. e−kxdx =1/k (k > 0)
0
� M
�
�
M
e−kxdx =(−1/k)e−kx � = (1/k)(1 − e−kM )
�
0 �
0
Taking the limit as M →∞, we find e−kM → 0 and
� ∞
e−kxdx =1/k
0
We rewrite this calculation more informally as follows,
� ∞ �∞
e−kxdx =(−1/k)e−kx � � = (1/k)(1 − e−k∞)=1/k (since k > 0)
�
0 0
� ∞
Note that the integral over the infinite interval e−kxdx = 1/k has an easier formula than the
0
� M
correspondingfiniteintegral e−kxdx = (1/k)(1−e−kM ). As a practical matter, for large M,the
0
term e−kM isnegligible,soeventhesimplerformula 1/k servesasagoodapproximationtothefinite
integral. Infinite integrals are often easier than finite ones, just as infinitesimals and derivatives are
easier than difference quotients.
Application: Replace x by t = time in seconds in Example 1.
R = rate of decay = number of atoms that decay per second at time 0.
At later times t> 0 the decay rate is Re−kt (smaller by an exponential factor e−kt)
Eventually (over time 0 ≤ t < ∞) every atom decays. So the total number of atoms N is
calculated using the formula we found in Example 1,
� ∞
N = Re−ktdt = R/k
0
The half life H of a radioactive element is the time H at which the decay rate is half what it was at
the start. Thus
e−kH =1/2 =⇒ −kH = ln(1/2) =⇒ k = (ln 2)/H
1

Lecture 35 18.01 Fall 2006
Hence
R = Nk = N(ln2)/H
Let us illustrate with Polonium 210, which has been in the news lately. The half life is 138 days
or
H = (138days)(24hr/day)(602sec/hr) = (138)(24)(60)2seconds
Using this value of H, we find that one gram of Polonium 210 emits (1 gram)(6 × 1023/210
atoms/gram)(ln2)/H =1.661014 decays/sec ≈ 4500 curies
At 5.3 MeV per decay, Polonium gives off 140 watts of radioactive energy per gram (white hot).
Poloniumemitsalpharays,whichareblockedbyskinbutwheningestedare 20 timesmoredangerous
than gamma and X-rays. The lethal dose, when ingested, is about 10−7 grams.
� ∞
Example 2. dx/(1 + x 2)= π/2.
0
We calculate,
� M dx
�
�
M
= tan−1 x� = tan−1 M →π/2
1+ x2 �
0 �
0
as M →∞. (If θ = tan−1 M then θ → π/2 as M →∞. See Figures 1 and 2.)
y = tan(x)
x = -π/2
.
M
x
θ
x = π/2
Figure 1: Graph of the tangent function, M = tan θ.
2

Lecture 35 18.01 Fall 2006
y = arctan(x)
y= π/2
θ
x = tan(y)
M
y = -π/2
�
�
�
�
�
�
�
�
�
�
�
�
�
�
�
�
�
�
.
Figure 2: Graph of the arctangent function, θ = tan−1 M.
∞ √
Example 3. e−x 2 dx = π/2
0
Recall that we already computed this improper integral (by computing a volume in two ways, slices
and the method of shells). This shows vividly that a finite integral can be harder to understand
than its infinite counterpart:
� M
e−x 2 dx
0
can only evaluated numerically. It has no elementary formula. By contrast, we found an explicit
formula when M = ∞.
� ∞
Example 4. dx/x
1
� M
M
dx/x = ln x = ln M − ln1 = ln M →∞
1
1
as M →∞. This improper integral is infinite (called divergent or not convergent).
∞
Example 5. dx/xp (p> 1)
1
� M
M
dx/xp = (1/(1 − p))x 1−p = (1/(1 − p))(M1−p − 1) → 1/(p − 1)
1
1
as M →∞ because 1 − p< 0. Thus, this integral is convergent.
∞
Example 6. dx/xp (0 <p< 1)
1
This is very similar to the previous example, but diverges
� M
M
dx/xp = (1/(1 − p))x 1−p = (1/(1 − p))(M1−p − 1) →∞
1
1
as M →∞ because 1 − p> 0.
3

Lecture 35 18.01 Fall 2006
Determining Divergence and Convergence
Todecidewhetheran integral converges ordiverges,don’t needto evaluate. Instead onecan compare
it to a simpler integral that can be evaluated.
� ∞ dx
The General Story for powers:
xp
1
From Examples 4, 5 and 6 we know that this diverges (is infinite) for 0 < p ≤ 1 and converges (is
finite) for p> 1.
The comparison of integrals says that a larger function has a larger integral. If we restrict
ourselves to nonnegative functions, then even when the region is unbounded, as in the case of an
improper integral, the area under the graph of the larger function is more than the area under the
graph of the smaller one. Consider 0 ≤ f(x) ≤ g(x) (as in Figure 3)
y
f(x) g(x)
x
x = a
Figure 3: The area under f(x) is less than the area under g(x) for a ≤ x< ∞.
� ∞ � ∞
If g(x) dx converges, then so does f(x) dx. (In other words, if the area under g is finite,
a a
then the area under f, being smaller, must also be finite.)
� ∞ � ∞
If f(x) dx diverges,thensodoes g(x) dx. (In other words, if the area under f isinfinite,
a a
then the area under g, being larger, must also be infinite.)
The way comparison is used is by replacing functions by simpler ones whose integrals we can
calculate. You will have to decide whether you want to trap the function from above or below. This
will depend on whether you are demonstrating that the integral is finite or infinite.
4

Lecture 35 18.01 Fall 2006
� ∞ dx
Example 7. √ It is natural to try the comparison
x3 +1
0
1 1
√ ≤
x3 +1 x3/2
But the area under x−3/2 on the interval 0 <x< ∞,
� ∞ dx
x3/2
0
turns out to be infinite because of the infinite behavior as x → 0. We can rescue this comparison by
excluding an interval near 0.
� ∞ dx � 1 dx � ∞ dx
√ = √ + √
x3 +1 x3 +1 x3 +1
0 0 1
Theintegral on 0 <x< 1 isafiniteintegralandthesecondintegral now works wellwith comparison,
� ∞ dx � ∞ dx
√ ≤ < ∞
x3 +1 x3/2
1 1
because 3/2 > 1.
� ∞
Example 8. e−x 3 dx
0
For x ≥ 1, x3 ≥ x, so
� ∞ � ∞
e−x 3 dx ≤ e−xdx =1 < ∞
1 1
Thus the full integral from 0 ≤ x < ∞ of e−x 3 converges as well. We can ignore the interval
0 ≤ x ≤ 1 because it has finite length and e−x 3 does not tend to infinity there.
Limit comparison:
Suppose that 0 ≤ f(x) and lim f(x)/g(x) ≤ 1. Then f(x) ≤ 2g(x) for x ≥ a (some large a).
x→∞
� ∞ � ∞
Hence f(x) dx ≤ 2 g(x) dx.
a a
� ∞ (x + 10) dx
Example 9.
x2 +1
0
The limiting behavior as x →∞ is
(x + 10)dx x 1
� =
x2 +1 x2 x
� ∞ dx � ∞ (x + 10) dx
Since = ∞, the integral also diverges.
x x2 +1
1 0
5

Lecture 35 18.01 Fall 2006
� ∞
Example 10 (from PS8). xn e−xdx
0
This converges. To carry out a convenient comparison requires some experience with growth rates
of functions.
x n << ex not enough. Instead use xn /ex/2 → 0 (true by L’Hop). It follows that
x n << ex/2 =⇒ xn e−x << ex/2 e−x = e−x/2
� ∞
Nowbylimitcomparison, since e−x/2dx converges, so does our integral. You will deal with this
0
integral on the problem set.
Improper Integrals of the Second Type
� 1 dx
√
x
0
1
We know that √ →∞ as x → 0.
x
� 1 dx � 1
√ = lim x−1/2dx
0 x a→0+ a
� 1 � 1
x−1/2dx =2x1 /2 � =2 − 2a 1/2
�
a a
As a →0, 2a1/2 → 0. So,
� 1
x−1/2 dx =2
0
Similarly,
� 1 1
x−pdx =
−p +1
0
for all p< 1.
1
For p = ,
2
1
=2
� �
1
− +1
2
However, for p ≥ 1, the integral diverges.
6

Lecture 36 18.01 Fall 2006
Lecture 36: Infinite Series and Convergence Tests
Infinite Series
Geometric Series
A geometric series looks like
1+ a + a 2 + a 3 + ... = S
There’s a trick to evaluate this: multiply both sides by a:
a + a2 + a 3 + ... = aS
Subtracting,
(1 + a + a2 + a 3 +··· ) − (a + a2 + a 3 + ··· )= S − aS
In other words,
1
1= S − aS =⇒ 1 = (1 − a)S =⇒ S =
1 − a
This only works when |a| < 1, i.e. −1 <a< 1.
a =1 can’t work:
1+1+1+ ... = ∞
a = −1 can’t work, either:
1 1
1 − 1+1 − 1+ ... =� =
1 − (−1) 2
Notation
Here is some notation that’s useful for dealing with series or sums. An infinite sum is written:
∞
�
a = a + a + a + ...
k 0 1 2
k=0
The finite sum
n
�
S = a = a + ... + a
n k 0 n
k=0
is called the “nth partial sum” of the infinite series.
1

Lecture 36 18.01 Fall 2006
Definition
∞
�
a = s
k
k=0
means the same thing as
n
�
lim S = s, where S = a
n n k
n→∞
k=0
We say the series converges to s, if the limit exists and is finite. The importance of convergence is
illustrated here by the example of the geometric series. If a =1,S =1+1+1+ ... = ∞. But
S − aS =1 or ∞−∞ =1
does not make sense and is not usable!
Another type of series:
�
∞
1
np
n=1
We can use integrals to decide if this type of series converges. First, turn the sum into an integral:
� ∞ 1 � ∞ dx
∼
np xp
n=1 1
If that improper integral evaluates to a finite number, the series converges.
Note: This approach only tells us whether or not a series converges. It does not tell us what
number the series converges to. That is a much harder problem. For example, it takes a lot of work
to determine
� ∞ 1 π2
=
n2 6
n=1
Mathematicians have only recently been able to determine that
�
∞
1
n3
n=1
converges to an irrational number!
Harmonic Series
� ∞ 1 � ∞ dx
∼
n x
n=1 1
We can evaluate the improper integral via Riemann sums.
We’ll use the upper Riemann sum (see Figure 1) to get an upper bound on the value of the
integral.
2

Lecture 36 18.01 Fall 2006
y=⁄x
1
½ 1
½
⅓
1 2 3
Figure 1: Upper Riemann Sum.
� N dx 1 1
≤ 1+ + ... + = s ≤ s
x 2 N − 1 N −1 N
1
We know that
� N dx
= ln N
x
1
As N →∞, ln N →∞, so s →∞ as well. In other words,
N
�
∞
1
n
n=1
diverges.
Actually, s approaches ∞ rather slowly. Let’s take the lower Riemann sum (see Figure 2).
N
y=⁄x
¼
½
⅓
1 2 3 4
Figure 2: Lower Riemann Sum.
1 1 � N 1 � N dx
s = 1 + + ... + = 1 + ≤ 1 + = 1 + ln N
N 2 N n x
n=2 1
Therefore,
ln N < s < 1 + ln N
N
3

Lecture 36 18.01 Fall 2006
Integral Comparison
1
Consider a positive, decreasing function f(x) > 0. (For example, f(x)= )
xp
� �
�� ∞ � ∞ �
� f(n) − f(x)dx� <f(1)
� �
� n=1 1 �
So, either both of the terms converge, or they both diverge. This is what we mean when we say
� ∞ 1 � ∞ dx
∼
np xp
n=1 1
�
∞
1
Therefore, diverges for p ≤ 1 and converges for p> 1.
np
n=1
Lots of fudge room: in comparison.
�
∞
1
√
n2 + 10
n=1
diverges, because
1 1 1
√ ∼ =
n2 + 10 (n2)1/2 n
Limit comparison:
� �
If f(x) ∼ g(x) as x →∞, then f(n) and g(n) either both converge or both diverge.
What, exactly, does f(x) ∼ g(x) mean? It means that
f(x)
lim = c
x→∞ g(x)
where 0 <c< ∞.
Let’s check: does the following series converge?
�
∞
n
√
n5 − 10
n=1
n n 1
√ ∼ = n−3/2 =
n5 − 10 n5/2 n3/2
3
Since > 1, this series does converge.
2
4

Lecture 36 18.01 Fall 2006
Playing with blocks
At this point in the lecture, the professor brings out several long, identical building blocks.
Do you think it’s possible to stack the blocks like this?
Top block is farther out
than the bottom block.
Figure 3: Collective center of mass of upper blocks is always over the base block.
In order for this to work, you want the collective center of mass of the upper blocks always to be
over the base block.
The professor successfully builds the stack.
Is it possible to extend this stack clear across the room?
The best strategy is to build from the top block down.
Let C be the left end of the first (top) block.
0
Let C = the center of mass of the first block (top block).
1
Put thesecond block asfarto theright aspossible, namely, sothatit’s leftendisat C (Figure 4).
1
Let C = the center of mass of the top two blocks.
2
Strategy: put the left end of the next block underneath the center of mass of all the previous ones
combined. (See Figure 5).
5

Lecture 36 18.01 Fall 2006
2
1/2
1
C C C
0 1 2
Figure 4: Stack of 2 Blocks.
2
1
2
3
1/2
1
1/3
C C C C
0 1 2 3
Figure 5: Stack of 3 Blocks. Left end of block 3 is C2 = center of mass of blocks 1 and 2.
C =0
0
C =1
1
1
C =1+
2 2
nC + 1(C +1) (n + 1)C +1 1
C = n n = n = C +
n+1 n +1 n +1 n n +1
1 1
C =1+ +
3 2 3
1 1 1
C =1+ + +
4 2 3 4
1 1 1 1
C =1+ + + + > 2
5 2 3 4 5
6

Lecture 36 18.01 Fall 2006
}
n
n+1 block
center of mass of
the first n blocks
Figure 6: Stack of n +1 Blocks.
Soyes,youcanextendthisstackasfar(horizontally)asyouwant —providedthatyouhaveenough
blocks. Another way of looking at this problem is to say
�
N
1
= S
n N
n=1
Recall the Riemann Sum estimation from the beginning of this lecture:
ln N <S < (ln N)+1
N
as N →∞, S →∞.
N
How high would this stack of blocks be if we extended it across the two lab tables here at the
front of the lecture hall? The blocks are 30 cm by 3 cm (see Figure 7). One lab table is 6.5 blocks,
or 13 units, long. Two tables are 26 units long. There will be 26 − 2 = 24 units of overhang in the
stack.
3 cm
30 cm
Figure 7: Side view of one block.
If ln N = 24, then N = e2 4 .
Height =3 cm· e2 4 ≈ 8 × 108 m
That height is roughly twice the distance to the moon.
If you want the stack to span this room (∼ 30 ft.), it would have to be 1026 meters high. That’s
about the diameter of the observable universe.
7

Lecture 37 18.01 Fall 2006
Lecture 37: Taylor Series
General Power Series
What is cos x anyway?
Recall: geometric series
1
1+ a + a2 +··· = for |a|< 1
1 − a
General power series is an infinite sum:
f(x)= a + a x + a x 2 + a x 3 + ···
0 1 2 3
represents f when |x| <R where R = radiusofconvergence. Thismeansthatfor |x| <R, |a xn|→ 0
n
as n → ∞ (“geometrically”). On the other hand, if |x| > R, then |a xn| does not tend to 0. For
n
1 1
example,inthecaseofthegeometricseries,if |a| = ,then |an | = . Since the higher-order terms
2 2n
get increasingly small if |a| < 1, the “tail” of the series is negligible.
Example 1. If a = −1, |an| =1 does not tend to 0.
1 − 1+1 − 1+ ···
The sum bounces back and forth between 0 and 1. Therefore it does not approach 0. Outside the
interval −1 <a< 1, the series diverges.
Basic Tools
Rules of polynomials apply to series within the radius of convergence.
Substitution/Algebra
1
=1+ x + x2 +···
1 − x
Example 2. x = -u.
1
=1 − u + u2 − u3 + ···
1+ u
Example 3. x = −v2 .
1
=1 − v 2 + v 4 − v 6 + ···
1 + v2
1

Lecture 37 18.01 Fall 2006
Example 4.
� �� �
1 1
= (1+ x + x2 + ··· )(1 + x + x2 + ··· )
1 − x 1 − x
Term-by-term multiplication gives:
1+2x +3x 2 + ···
1
Remember, here x is some number like . As you take higher and higher powers of x, the result
2
gets smaller and smaller.
Differentiation (term by term)
d
�
1
�
= d � 1+ x + x2 + x3 + ··· �
dx 1 − x dx
1
=0+1+2x +3x2 + ··· where 1 is a , 2 is a and 3 is a
(1 − x)2 0 1 2
Same answer as Example 4, but using a new method.
Integration (term by term)
� � a a �
f(x) dx = c + a + 1 x 2 + 2 x 3 +···
0 2 3
where
f(x)= a + a x + a x 2 + ···
0 1 2
� du
Example 5.
1+ u
� �
1
=1 − u + u2 − u3 + ···
1 + u
� du u2 u3 u4
= c + u − + − + ···
1+ u 2 3 4
� x du x2 x3 x4
ln(1 + x)= = x − + +
1+ u 2 3 4
0
So now we know the series expansion of ln(1 + x).
Example 6. Integrate Example 3.
1
=1 − v 2 + v 4 − v 6 + ···
1+ v2
� dv � v3 v5 v7 �
= c + v − + − + ···
1+ v2 3 5 7
� x dv x3 x5 x7
tan−1 x = = x − + − + ···
1+ v2 3 5 7
0
2

Lecture 37 18.01 Fall 2006
Taylor’s Series and Taylor’s Formula
If f(x)= a + a x + a x2 + ··· , we want to figure out what all these coefficients are.
0 1 2
Differentiating,
f�(x)= a +2a x +3a x 2 + ···
1 2 3
f��(x) = (2)(1)a + (3)(2)a x + (4)(3)a x2 + ···
2 3 4
f���(x) = (3)(2)(1)a + (4)(3)(2)a x + ···
3 4
Let’s plug in x =0 to all of these equations.
f(0) = a ; f�(0) = a ; f��(0) = 2a ; f���(0) = (3!)a
0 1 2 3
Taylor’s Formula tells us what the coefficients are:
f(n)(0) = (n!)a
n
Remember, n!= n(n − 1)(n − 2) ··· (2)(1) and 0! = 1. Coefficients a are given by:
n
� �
1
a = f(n)(0)
n n!
Example 7. f(x)= ex.
f�(x)= e x
f��(x)= e x
f(n)(x)= e x
f(n)(0) = e 0 =1
1
Therefore, by Taylor’s Formula a = and
n n!
1 1 1 1
ex = + x + x2 + x3 +···
0! 1! 2! 3!
Or in compact form,
� ∞ xn
e x =
n!
n=0
Now, we can calculate e to any accuracy:
1 1 1 1
e =1+1+ + + + +···
2 3! 4! 5!
Example 7. f(x) = cos x.
f�(x)= − sin x
f��(x)= − cos x
3

Lecture 37 18.01 Fall 2006
f���(x) = sin x
f(4)(x) = cos x
f(0) = cos(0) = 1
f�(0) = − sin(0) = 0
f��(0) = − cos(0) = −1
f���(0) = sin(0) = 0
Only even coefficients are non-zero, and their signs alternate. Therefore,
1 1 1 1
cos x =1 − x 2 + x 4 − x6 + x 8 + ···
2 4! 6! 8!
Note: cos(x) is an even function. So is this power series — as it contains only even powers of x.
TherearetwowaysoffindingtheTaylorSeriesfor sin x. Take derivative of cos x, oruseTaylor’s
formula. We will take the derivative:
� �
d 1 4 6 8
− sin x = cos x =0 − 2 x + x 3 − x5 + x 7 + ···
dx 2 4! 6! 8!
x3 x5 x7
= −x + − + + ···
3! 5! 7!
x3 x5 x7
sin(x)= x − + − +···
3! 5! 7!
Compare with quadratic approximation from earlier in the term:
1
cos x ≈ 1 − x2 sin x ≈ x
2
We can also write:
� ∞ x2k x0 x2 1
cos x = (−1)k =(−1)0 +(−1)2 + ··· =1 − x 2 +···
(2k)! 0! 2! 2
k=0
� ∞ x2k+1
sin x = (−1)k ← n =2k +1
(2k + 1)!
k=0
Example 8: Binomial Expansion. f(x) = (1+ x)a
a a(a − 1) a(a − 1)(a − 2)
(1 + x)a =1+ x + x 2 + x 3 +···
1 2! 3!
4

Lecture 37 18.01 Fall 2006
Taylor Series with Another Base Point
A Taylor series with its base point at a (instead of at 0) looks like:
f��(b) f(3)(b)
f(x)= f(b)+ f�(b)(x − b)+ (x − b)2 + (x − b)3 + ...
2 3!
√ √
Taylorseriesfor x. It’s a bad idea to expand using b =0 because x isnotdifferentiableat x =0.
Instead use b =1.
� �� �
1 1
− 1
1 2 2
x 1/2 =1+ (x − 1)+ (x − 1)2 + ···
2 2!
5

Lecture 38 18.01 Fall 2006
Lecture 38: Final Review
Review: Differentiating and Integrating Series.
∞
�
If f(x)= a x n, then
n
n=0
f�(x)= � ∞ na x n−1 and � f(x)dx = C + � ∞ a n xn+1
n n +1
n=1 n=0
Example 1: Normal (or Gaussian) Distribution.
� x � x � (−t2)2 (−t2)3 �
e−t2 dt = 1 − t2 + + + ··· dt
2! 3!
0 0
� x � t4 t6 t8 �
= 1 − t2 + − + − ... dt
2! 3! 4!
0
x3 1 x5 1 x7
= x − + − + ...
3 2! 5 3! 7
� x
Even though
e−t2
dt isn’t an elementary function, we can still compute it. Elementary functions
0
are still a little bit better, though. For example:
x3 x5 π π (π/2)3 (π/2)5
sin x = x − + −··· =⇒ sin = − + −···
3! 5! 2 2 3! 5!
But to compute sin(π/2) numerically is a waste of time. We know that the sum if something very
simple, namely,
π
sin =1
2
It’s not obvious from the series expansion that sin x deals with angles. Series are sometimes com­
plicated and unintuitive.
π π
Nevertheless, we can read this formula backwards to find a formula for . Start with sin =1.
2 2
Then,
� 1 dx �1 π π
√ = sin−1 x� = sin−1 1 − sin−1 0= − 0=
0 1 − x2 � 0 2 2
We want to find the series expansion for (1 − x2)−1/2, but let’s tackle a simpler case first:
� �� � � �� �� �
1 1 1 1 1
− − − 1 − − − 1 − − 2
� �
1 2 2 2 2 2
(1 + u)−1/2 =1+ − u + u 2 + u3 + ···
2 1· 2 1·2· 3
1 1· 3 1· 3· 5
=1 − u + u 2 − u3 + ···
2 2 · 4 2 ·4 · 6
Notice the pattern: odd numbers go on the top, even numbers go on the bottom, and the signs
alternate.
1

Lecture 38 18.01 Fall 2006
Now, let u = −x2 .
1 1· 3 1· 3· 5
(1 − x 2)−1/2 =1+ x 2 + x 4 + x 6 + ···
2 2 · 4 2 ·4 · 6
� � 1 x3 1· 3 x5 1· 3· 5 x7 �
(1 − x 2)−1/2dx = C + x + + + + ···
2 3 2 · 4 5 2 ·4 · 6 7
π � 1 1 � 1 � � 1· 3 �� 1 � � 1· 3· 5 �� 1 �
= (1 − x 2)−1/2dx =1+ + + + ···
2 2 3 2 · 4 5 2 ·4 · 6 7
0
Here’s a hard (optional) extra credit problem: why does this series converge? Hint: use
L’Hôpital’s rule to find out how quickly the terms decrease.
The Final Exam
Here’s another attempt to clarify the concept of weighted averages.
Weighted Average
A weighted average of some function, f, is defined as:
�b
w(x)f(x) dx
Average(f)= a
�b
w(x) dx
a
� b
Here, w(x) dx is the total, and w(x) is the weighting function.
a
Example: taken from a past problem set.
You get $t if a certain particle decays in t seconds. How much should you pay to play? You were
given that the likelihood that the particle has not decayed (the weighting function) is:
w(x)= e−kt
Remember,
� ∞ 1
e−kt dt =
k
0
The payoff is
f(t)= t
The expected (or average) payoff is
�∞ f(t)w(t) dt �∞ te−kt dt
0 = 0
�∞
w(t) dt
�∞
e−kt dt
0 0
� ∞ � ∞
= k te−kt dt = (kt)e−kt dt
0 0
Do the change of variable:
u = kt and du = k dt
2

Lecture 38 18.01 Fall 2006
� ∞ du
Average = ue−u
k
0
� ∞
On a previous problem set, you evaluated this using integration by parts: ue−u du =1.
0
� ∞ du 1
Average = ue−u =
k k
0
Ontheproblemset, wecalculatedthehalf-life(H)forPolonium120 was (131)(24)(60)2 seconds. We
also found that
ln2
k =
H
Therefore, the expected payoff is
1 H
=
k ln2
where H is the half-life of the particle in seconds.
Now, you’re all probably wondering: who on earth bets on particle decays?
In truth, no one does. There is, however, a very similar problem that is useful in the real world.
There is something called an annuity, which is basically a retirement pension. You can buy an
annuity, and then get paid a certain amount every month once you retire. Once you die, the annuity
payments stop.
You (and the people paying you) naturally care about how much money you can expect to get
over the course of your retirement. In this case, f(t) = t represents how much money you end up
with, and w(t)= e−kt represents how likely your are to be alive after t years.
What if you want a 2-life annuity? Then, you need multiple integrals, which you will learn about
in multivariable calculus (18.02).
Our first goal in this class was to be able to differentiate anything. In multivariable calculus, you
will learn about another chain rule. That chain rule will unify the (single-variable) chain rule, the
product rule, the quotient rule, and implicit differentiation.
You might say the multivariable chain rule is
One thing to rule them all
One thing to find them
One thing to bring them all
And in a matrix bind them.
(with apologies to JRR Tolkien).
3

