# MIT 18.01 Single Variable Calculus - Unit 1: Derivatives

> Source: MIT OpenCourseWare, http://ocw.mit.edu
> Collected: 2026-05-29
> Published: Fall 2006

MIT OpenCourseWare
http://ocw.mit.edu
18.01 Single Variable Calculus
Fall 2006

## Lecture 1: Derivatives, Slope, Velocity, and Rate of Change

Unit 1: Derivatives
A. What is a derivative?
- Geometric interpretation
- Physical interpretation
- Important for any measurement (economics, political science, finance, physics, etc.)
B. How to differentiate any function you know.

The derivative is the slope of the line tangent to the graph of $f(x)$. It is NOT just a line that meets the graph at one point. It is the limit of the secant line (a line drawn between two points on the graph) as the distance between the two points goes to zero.

Geometric definition of the derivative: Limit of slopes of secant lines $PQ$ as $Q \to P$ ($P$ fixed). The slope of $PQ$:

$$\frac{\Delta f}{\Delta x} = \frac{f(x_0 + \Delta x) - f(x_0)}{\Delta x} \to f'(x_0) \quad (\text{as } \Delta x \to 0)$$

"difference quotient" $\to$ "derivative of $f$ at $x_0$"

**Example 1.** $f(x) = 1/x$

$$\frac{\Delta f}{\Delta x} = \frac{\frac{1}{x_0 + \Delta x} - \frac{1}{x_0}}{\Delta x} = \frac{-1}{(x_0 + \Delta x)x_0}$$

Taking the limit as $\Delta x \to 0$:

$$f'(x_0) = -\frac{1}{x_0^2}$$

Notice that $f'(x_0)$ is negative — as is the slope of the tangent line.

**Finding the tangent line:** $y - y_0 = f'(x_0)(x - x_0)$

For $f(x) = 1/x$ at $x_0$: $y - \frac{1}{x_0} = \left(-\frac{1}{x_0^2}\right)(x - x_0)$

The tangent line forms a triangle with the $x$- and $y$-axes. The $x$-intercept is at $x = 2x_0$ and the $y$-intercept is at $y = 2y_0$. The area of this triangle is always $2$, no matter where on the graph we draw the tangent line.

**Notations for the derivative:**
- Leibniz' notation: $\frac{dy}{dx}$
- Newton's notation: $f'(x_0)$
- Other: $\frac{df}{dx}$, $\dot{f}$, $Df$

**Example 2.** $f(x) = x^n$ where $n = 1, 2, 3, \dots$

Using the binomial theorem:

$$(x + \Delta x)^n = x^n + n(\Delta x)x^{n-1} + O\!\left((\Delta x)^2\right)$$

Therefore:

$$\frac{d}{dx}(x^n) = nx^{n-1}$$

This extends to polynomials:

$$\frac{d}{dx}(x^2 + 3x^{10}) = 2x + 30x^9$$

**Physical interpretation:** The derivative represents a rate of change. Example: pumpkin drop from $400$ ft — $y = 400 - 16t^2$. Average speed $= 80$ ft/s. Instantaneous velocity at $t = 5$: $y' = -32t = -160$ ft/s (about $110$ mph).

## Lecture 2: Limits, Continuity, and Trigonometric Limits

$$\frac{\Delta y}{\Delta x} \to \frac{dy}{dx} \text{ as } \Delta x \to 0$$

Average rate of change $\to$ Instantaneous rate of change.

**Examples of derivatives as rates:**
1. $\frac{dq}{dt} =$ electrical current ($q =$ charge)
2. $\frac{ds}{dt} =$ speed ($s =$ distance)
3. $\frac{dT}{dx} =$ temperature gradient ($T =$ temperature)
4. GPS sensitivity: how accurately can we measure $L$ given changes in $h$

**Easy Limits:**

$$\lim_{x \to 3} \frac{x^2 + x}{x + 1} = \frac{9 + 3}{4} = 3$$

**Continuity:** $f(x)$ is continuous at $x_0$ when $\displaystyle\lim_{x \to x_0} f(x) = f(x_0)$.

**Types of Discontinuity:**
1. Removable discontinuity — left and right limits exist and are equal, but not equal to $f(x_0)$
2. Jump discontinuity — left and right limits exist but are NOT equal
3. Infinite discontinuity — limits go to $\pm\infty$ (e.g., $1/x$ at $x = 0$)
4. Ugly discontinuities — oscillatory behavior, limit does not exist

**Derivative of $1/x$:** $f(x) = 1/x$, $f'(x) = -1/x^2$. Note: $f(x)$ is odd, $f'(x)$ is even. The derivative of an odd function is always even, and vice versa.

**Two Trigonometric Limits ($\theta$ in radians):**

$$\lim_{\theta \to 0} \frac{\sin\theta}{\theta} = 1 \qquad \lim_{\theta \to 0} \frac{1 - \cos\theta}{\theta} = 0$$

**Theorem: Differentiable Implies Continuous.** If $f$ is differentiable at $x_0$, then $f$ is continuous at $x_0$.

Proof:

$$\lim_{x \to x_0} \bigl(f(x) - f(x_0)\bigr) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0} (x - x_0) = f'(x_0) \cdot 0 = 0$$

## Lecture 3: Derivatives of Products, Quotients, Sine, and Cosine

**Derivative Formulas:**
1. Specific: $\frac{d}{dx}(x^n)$ or $\frac{d}{dx}\!\left(\frac{1}{x}\right)$
2. General: $(u + v)' = u' + v'$ and $(cu)' = cu'$ ($c$ constant)

**Derivatives of $\sin x$ and $\cos x$:**

$$\frac{d}{dx}\sin x = \cos x \qquad \frac{d}{dx}\cos x = -\sin x$$

Proof for $\sin x$:

$$\frac{d}{dx}\sin x = \lim_{\Delta x \to 0} \frac{\sin(x + \Delta x) - \sin x}{\Delta x}$$

Using $\sin(a + b) = \sin a \cos b + \cos a \sin b$:

$$= \lim_{\Delta x \to 0} \frac{\sin x(\cos\Delta x - 1) + \cos x \sin\Delta x}{\Delta x}$$

$$= \sin x \cdot \lim_{\Delta x \to 0} \frac{\cos\Delta x - 1}{\Delta x} + \cos x \cdot \lim_{\Delta x \to 0} \frac{\sin\Delta x}{\Delta x} = \sin x \cdot 0 + \cos x \cdot 1 = \cos x$$

**Product Rule:** $(uv)' = u'v + uv'$

Proof: Add $u(x + \Delta x)v(x) - u(x + \Delta x)v(x) = 0$ to the numerator of the difference quotient, then rearrange and take limits.

Intuitive justification: area of rectangle $(u + \Delta u)(v + \Delta v) - uv \approx u\Delta v + v\Delta u$ when $\Delta u, \Delta v$ are small.

**Quotient Rule:** $\displaystyle\left(\frac{u}{v}\right)' = \frac{u'v - uv'}{v^2}$

## Lecture 4: Chain Rule, and Higher Derivatives

**Chain Rule:**

$$\frac{dy}{dt} = \frac{dy}{dx}\frac{dx}{dt} \quad \text{or} \quad \frac{d}{dx}f(g(x)) = f'(g(x))\,g'(x)$$

Example: $y = \sin x$, $x = t^2$ $\to$ $\displaystyle\frac{d}{dt}\sin(t^2) = (\cos x)(2t) = 2t\cos(t^2)$

Composition is not commutative: $f \circ g \neq g \circ f$.

**Example:** $\displaystyle\frac{d}{dx}\cos\!\left(\frac{1}{x}\right)$

Let $u = 1/x$. Then $\displaystyle\frac{dy}{dx} = \frac{dy}{du}\frac{du}{dx} = (-\sin u)\!\left(-\frac{1}{x^2}\right) = \frac{\sin(1/x)}{x^2}$

**Higher Derivatives:**

- $f'(x)$, $Df$, $\dfrac{df}{dx}$ — first derivative
- $f''(x)$, $D^2f$, $\dfrac{d^2f}{dx^2}$ — second derivative
- $f^{(n)}(x)$, $D^nf$, $\dfrac{d^nf}{dx^n}$ — $n$th derivative

$$D^n x^n = n! \quad (\text{$n$ factorial})$$

Proof by induction: base case $n = 1$ gives $Dx = 1$; inductive step uses $D^{n+1}x^{n+1} = D^n((n+1)x^n) = (n+1)n! = (n+1)!$.

## Lecture 5: Implicit Differentiation and Inverses

**Implicit Differentiation:** Extending $\displaystyle\frac{d}{dx}(x^a) = ax^{a-1}$ to rational exponents.

For $y = x^{m/n}$: $y^n = x^m$. Differentiating:

$$ny^{n-1}\frac{dy}{dx} = mx^{m-1} \quad\Rightarrow\quad \frac{dy}{dx} = \frac{m}{n}x^{m/n - 1}$$

**Example: Circle** $x^2 + y^2 = 1$

$$2x + 2y\frac{dy}{dx} = 0 \quad\Rightarrow\quad \frac{dy}{dx} = -\frac{x}{y}$$

**Example:** $y^3 + xy^2 + 1 = 0$

$$3y^2\frac{dy}{dx} + y^2 + 2xy\frac{dy}{dx} = 0 \quad\Rightarrow\quad \frac{dy}{dx} = \frac{-y^2}{3y^2 + 2xy}$$

**Inverse Functions:** If $y = f(x)$ and $g(y) = x$, then $g$ is the inverse function $f^{-1}$.

$$\frac{d}{dx}\bigl(f^{-1}(y)\bigr) = \frac{1}{\frac{dy}{dx}}$$

**Example:** $y = \arctan x$

$$\tan y = x \quad\Rightarrow\quad \sec^2 y \frac{dy}{dx} = 1 \quad\Rightarrow\quad \frac{dy}{dx} = \cos^2(\arctan x) = \frac{1}{1 + x^2}$$

Using a right triangle with angle $y$ where $\tan y = x$, the hypotenuse is $\sqrt{1 + x^2}$, so $\cos y = 1/\sqrt{1 + x^2}$.

## Lecture 6: Exponential and Log, Logarithmic Differentiation, Hyperbolic Functions

**Derivative of $a^x$:**

$$\frac{d}{dx}(a^x) = M(a)\,a^x$$

where $\displaystyle M(a) = \lim_{\Delta x \to 0} \frac{a^{\Delta x} - 1}{\Delta x}$.

**The number $e$:** Defined as the unique number such that $M(e) = 1$, i.e.,

$$\frac{d}{dx}(e^x) = e^x$$

**Natural log:**

$$\frac{d}{dx}\ln x = \frac{1}{x}$$

**Derivative of $a^x$ (general):**

$$\frac{d}{dx}(a^x) = \ln a \cdot a^x$$

**Logarithmic Differentiation:** $(\ln f)' = f'/f$, so $f' = f\cdot(\ln f)'$ .

**Example:** $\displaystyle\frac{d}{dx}(x^x) = x^x\bigl(\ln x + 1\bigr)$

**Key Limit:**

$$\lim_{k \to \infty}\left(1 + \frac{1}{k}\right)^k = e$$

**Hyperbolic Functions:**

- $\displaystyle\sinh x = \frac{e^x - e^{-x}}{2}$, $\displaystyle\frac{d}{dx}\sinh x = \cosh x$
- $\displaystyle\cosh x = \frac{e^x + e^{-x}}{2}$, $\displaystyle\frac{d}{dx}\cosh x = \sinh x$
- Identity: $\cosh^2 x - \sinh^2 x = 1$ (hyperbola) vs $\cos^2 x + \sin^2 x = 1$ (circle)

## Lecture 7: Continuation and Exam Review

**General Differentiation Formulas:**

- $(u + v)' = u' + v'$
- $(cu)' = cu'$
- $(uv)' = u'v + uv'$
- $\displaystyle\left(\frac{u}{v}\right)' = \frac{u'v - uv'}{v^2}$
- $\displaystyle\frac{d}{dx}f(u(x)) = f'(u(x))\,u'(x)$

**Specific differentiation formulas:** $x^n$, $\sin^{-1}x$, $\tan^{-1}x$, $\sin x$, $\cos x$, $\tan x$, $\sec x$, $e^x$, $\ln x$.

$$\frac{d}{dx}\sec x = \tan x \sec x$$

**For real $r$:**

$$\frac{d}{dx}(x^r) = r x^{r-1}$$

(Proved using base $e$: $x^r = e^{r\ln x}$, or by logarithmic differentiation.)

**Example:**

$$\frac{d}{dx}\!\left(e^{x\tan^{-1} x}\right) = e^{x\tan^{-1} x}\!\left(\tan^{-1} x + \frac{x}{1 + x^2}\right)$$
