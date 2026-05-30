# MIT 18.01 Single Variable Calculus — Unit 4: Techniques of Integration and Series

> Sources: MIT OpenCourseWare, Fall 2006
> Raw: [MIT 18.01 Unit 4 Integration and Series](../../raw/learning/mit-18.01-unit4-integration-and-series.md)

## Overview

The fourth and final unit of MIT's 18.01 Single Variable Calculus (Fall 2006, taught by Professor David Jerison) rounds out the course with advanced integration techniques and the theory of series. Topics include trigonometric integrals and substitutions, partial fractions, integration by parts, arc length, surface area, polar coordinates, L'Hôpital's rule, improper integrals, infinite series, and Taylor series.

## Trigonometric Integrals

### Products of $\sin^n x \cos^m x$

**Method A** (at least one of $n$, $m$ is odd): Save one factor of the odd-powered function for $du$, convert the rest using $\sin^2 x + \cos^2 x = 1$, and substitute.

Example: $\int \sin^3 x \cos^2 x\,dx$. Let $u = \cos x$, $du = -\sin x\,dx$:

$$\int \sin^3 x \cos^2 x\,dx = \int (1 - \cos^2 x)\cos^2 x \sin x\,dx = -\frac{1}{3}\cos^3 x + \frac{1}{5}\cos^5 x + C$$

**Method B** (both $n$ and $m$ even): Use double-angle identities:

$$\cos^2 x = \frac{1 + \cos 2x}{2}, \qquad \sin^2 x = \frac{1 - \cos 2x}{2}$$

Apply Method B repeatedly until a term with an odd power appears, then switch to Method A.

### Products of $\sec^n x \tan^m x$

Key identity: $\sec^2 x = 1 + \tan^2 x$.

Standard integrals:
- $\int \tan x\,dx = -\ln|\cos x| + C$
- $\int \sec x\,dx = \ln|\sec x + \tan x| + C$ (by "advanced guessing": multiply by $\frac{\sec x + \tan x}{\sec x + \tan x}$)
- $\int \sec^2 x\,dx = \tan x + C$
- $\int \sec x \tan x\,dx = \sec x + C$

For even powers of $\sec$: substitute $u = \tan x$, $du = \sec^2 x\,dx$.
For odd powers of $\tan$: substitute $u = \sec x$, $du = \sec x \tan x\,dx$.

## Trigonometric Substitution

Three patterns for integrals involving square roots:

| Integral form | Substitution | Identity |
|---------------|-------------|----------|
| $\sqrt{a^2 - x^2}$ | $x = a\sin u$ | $1 - \sin^2 u = \cos^2 u$ |
| $\sqrt{a^2 + x^2}$ | $x = a\tan u$ | $\tan^2 u + 1 = \sec^2 u$ |
| $\sqrt{x^2 - a^2}$ | $x = a\sec u$ | $\sec^2 u - 1 = \tan^2 u$ |

After integrating in $u$, convert back to $x$ using a right triangle.

### Example: $\int_0^x \sqrt{a^2 - t^2}\,dt$

Let $t = a\sin u$, $dt = a\cos u\,du$. Then:

$$\int_0^x \sqrt{a^2 - t^2}\,dt = \frac{a^2}{2}\sin^{-1}\left(\frac{x}{a}\right) + \frac{1}{2}x\sqrt{a^2 - x^2}$$

Geometrically, this is the sum of a circular sector $\frac{1}{2}a^2 u$ and a triangle $\frac{1}{2}x\sqrt{a^2 - x^2}$.

### Completing the Square

For integrals with $\sqrt{x^2 + bx + c}$, complete the square first:

$$x^2 + 4x = (x+2)^2 - 4$$

Then substitute $v = x + 2$, and use a trigonometric substitution on $\sqrt{v^2 - 4}$.

## Partial Fractions

A method for integrating rational functions $P(x)/Q(x)$.

1. If degree of $P$ $\ge$ degree of $Q$, perform long division first.
2. Factor $Q$ into linear and irreducible quadratic factors.
3. Decompose into partial fractions.

### Cover-Up Method

For distinct linear factors $(x - a)(x - b)$, find coefficients rapidly:

$$\frac{4x - 1}{(x-1)(x+2)} = \frac{A}{x-1} + \frac{B}{x+2}$$

Multiply by $(x-1)$, set $x = 1$: $A = \frac{4(1)-1}{1+2} = 1$.
Multiply by $(x+2)$, set $x = -2$: $B = \frac{4(-2)-1}{-2-1} = 3$.

### Repeated Factors

For $\frac{x^2 + 2}{(x-1)^2(x+2)}$:

$$\frac{x^2 + 2}{(x-1)^2(x+2)} = \frac{A}{x-1} + \frac{B}{(x-1)^2} + \frac{C}{x+2}$$

$B$ and $C$ are found by cover-up; $A$ by plugging a convenient value (e.g., $x=0$).

### Irreducible Quadratics

For $(x^2 + 1)(x-1)$ in the denominator:

$$\frac{1}{(x^2+1)(x-1)} = \frac{A}{x-1} + \frac{Bx + C}{x^2+1}$$

Cover-up gives $A$; the remaining coefficients come from plugging values like $x=0$ and $x=-1$.

## Integration by Parts

From the product rule: $\int uv'\,dx = uv - \int u'v\,dx$, or equivalently $\int u\,dv = uv - \int v\,du$.

### Examples

- $\int \tan^{-1} x\,dx = x\tan^{-1} x - \frac{1}{2}\ln(1+x^2) + C$ (take $u = \tan^{-1} x$, $v' = 1$)
- $\int \ln x\,dx = x\ln x - x + C$

### Reduction Formulae

Repeated integration by parts yields recurrence relations:

$$\int (\ln x)^n\,dx = x(\ln x)^n - n\int (\ln x)^{n-1}\,dx$$

$$\int x^n e^x\,dx = x^n e^x - n\int x^{n-1} e^x\,dx$$

## Arc Length

The infinitesimal arc length $ds$ satisfies $(ds)^2 = (dx)^2 + (dy)^2$. Depending on the representation:

$$ds = \sqrt{1 + (dy/dx)^2}\,dx = \sqrt{(dx/dt)^2 + (dy/dt)^2}\,dt = \sqrt{(dx/dy)^2 + 1}\,dy$$

### Example: Circle

For $y = \sqrt{1 - x^2}$:

$$ds = \sqrt{1 + \left(\frac{-x}{\sqrt{1-x^2}}\right)^2}\,dx = \frac{dx}{\sqrt{1-x^2}}$$

So the arc length from $0$ to $a$ is $\int_0^a \frac{dx}{\sqrt{1-x^2}} = \sin^{-1} a$, which is precisely the angle (in radians).

### Parametric Curves

A curve given by $x = f(t)$, $y = g(t)$ has:

$$ds = \sqrt{(dx/dt)^2 + (dy/dt)^2}\,dt$$

Example: $x = t^2$, $y = t^3$ ($0 \le t \le 1$):

$$\text{Length} = \int_0^1 \sqrt{4t^2 + 9t^4}\,dt = \int_0^1 t\sqrt{4+9t^2}\,dt = \frac{1}{27}(13^{3/2} - 4^{3/2})$$

## Surface Area of Revolution

When a curve is revolved around the $x$-axis, the surface area element is $2\pi y\,ds$:

$$A = \int 2\pi y\,ds$$

### Example: Surface Area of a Sphere

For the unit sphere, $y = \sqrt{1-x^2}$ and $ds = dx/\sqrt{1-x^2}$:

$$A = \int_a^b 2\pi\sqrt{1-x^2}\cdot\frac{dx}{\sqrt{1-x^2}} = 2\pi(b-a)$$

For the whole sphere ($a=-1$, $b=1$): $A = 4\pi$.

## Polar Coordinates

$$x = r\cos\theta, \qquad y = r\sin\theta$$

### Example: Circle off-center

The circle $(x-a)^2 + y^2 = a^2$ has polar equation $r = 2a\cos\theta$ (for $-\pi/2 < \theta < \pi/2$).

### Area in Polar Coordinates

A small sector has area $\frac{1}{2}r^2\,d\theta$, so:

$$A = \int_{\theta_1}^{\theta_2} \frac{1}{2}r^2\,d\theta$$

For the circle $r = 2a\cos\theta$:

$$A = \int_{-\pi/2}^{\pi/2} \frac{1}{2}(2a\cos\theta)^2\,d\theta = 2a^2\int_{-\pi/2}^{\pi/2} \cos^2\theta\,d\theta = \pi a^2$$

## L'Hôpital's Rule

For limits of the form $0/0$ or $\infty/\infty$:

$$\lim_{x\to a} \frac{f(x)}{g(x)} = \lim_{x\to a} \frac{f'(x)}{g'(x)}$$

provided the latter limit exists (and $g'(a) \neq 0$ in the simplest case). The rule also applies for $x \to \infty$ and can be applied repeatedly.

### Examples

- $\displaystyle\lim_{x\to 1}\frac{x^{15} - 1}{x^3 - 1} = \frac{15}{3} = 5$
- $\displaystyle\lim_{x\to 0}\frac{\cos x - 1}{x^2} = -\frac{1}{2}$
- $\displaystyle\lim_{x\to\infty}\frac{e^{ax}}{x^{10}} = \infty$ (for $a > 0$): exponentials dominate polynomials
- $\displaystyle\lim_{x\to\infty}\frac{\ln x}{x^{1/3}} = 0$: logarithms grow slower than any positive power

### Other Indeterminate Forms

For $1^\infty$, $0^0$, $0\cdot\infty$: rewrite using exponentials and logarithms.

Example: $\displaystyle\lim_{x\to 0^+} x^x$. Write as $e^{x\ln x}$, then:

$$\lim_{x\to 0^+} x\ln x = \lim_{x\to 0^+} \frac{\ln x}{1/x} = \lim_{x\to 0^+} \frac{1/x}{-1/x^2} = \lim_{x\to 0^+} (-x) = 0$$

Hence $\lim_{x\to 0^+} x^x = e^0 = 1$.

**Warning**: Always check the limit form before applying L'Hôpital's rule. Applying it to $\lim_{x\to 0} \frac{\sin x}{x^2}$ gives the wrong answer because the limit is of the form $1/0$, not $0/0$.

## Improper Integrals

An improper integral has an infinite limit of integration or an integrand that blows up within the interval.

$$\int_a^\infty f(x)\,dx = \lim_{M\to\infty} \int_a^M f(x)\,dx$$

### Key Examples

- $\int_0^\infty e^{-kx}\,dx = 1/k$ ($k > 0$)
- $\int_0^\infty \frac{dx}{1+x^2} = \pi/2$
- $\int_{-\infty}^\infty e^{-x^2}\,dx = \sqrt{\pi}$
- $\int_1^\infty \frac{dx}{x^p}$ converges for $p > 1$, diverges for $p \le 1$
- $\int_0^1 \frac{dx}{x^p}$ converges for $p < 1$, diverges for $p \ge 1$

### Comparison Test

If $0 \le f(x) \le g(x)$ on $[a, \infty)$:
- If $\int_a^\infty g$ converges, then $\int_a^\infty f$ converges.
- If $\int_a^\infty f$ diverges, then $\int_a^\infty g$ diverges.

### Application: Radioactive Decay

Polonium-210 has half-life $H = 138$ days. Decay rate: $R(t) = R_0 e^{-kt}$ where $k = \ln 2 / H$. Total number of atoms: $N = \int_0^\infty R_0 e^{-kt}\,dt = R_0/k$. One gram emits about 4500 curies and produces 140 watts of thermal energy.

## Infinite Series

A series $\sum_{k=0}^\infty a_k$ converges to $s$ if the sequence of partial sums $S_n = \sum_{k=0}^n a_k$ satisfies $\lim_{n\to\infty} S_n = s$.

### Geometric Series

$$\sum_{k=0}^\infty a^k = \frac{1}{1-a} \quad \text{for } |a| < 1$$

### Integral Test

For a positive decreasing function $f$:

$$\sum_{n=1}^\infty f(n) \quad \text{and} \quad \int_1^\infty f(x)\,dx$$

either both converge or both diverge.

### p-Series

$$\sum_{n=1}^\infty \frac{1}{n^p} \quad \text{converges for } p > 1, \text{ diverges for } p \le 1$$

The harmonic series ($p=1$) diverges: $\sum_{n=1}^\infty 1/n = \infty$, with partial sums bounded by $\ln N < S_N < 1 + \ln N$.

### Limit Comparison

If $\lim_{n\to\infty} a_n/b_n = c$ where $0 < c < \infty$, then $\sum a_n$ and $\sum b_n$ either both converge or both diverge.

### Block Stacking Problem

By placing blocks so that each is positioned with its left end at the center of mass of all blocks above it, the total overhang of $N$ blocks is:

$$C_N = \sum_{n=1}^N \frac{1}{n}$$

Since this is the harmonic series, the overhang grows like $\ln N$. To span the observable universe would require a stack roughly $10^{26}$ meters high.

## Taylor Series

A function can be represented as a power series about $x = 0$:

$$f(x) = a_0 + a_1 x + a_2 x^2 + a_3 x^3 + \cdots$$

where the coefficients are given by $a_n = \frac{f^{(n)}(0)}{n!}$.

### Key Expansions

$$e^x = \sum_{n=0}^\infty \frac{x^n}{n!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots$$

$$\cos x = \sum_{k=0}^\infty (-1)^k \frac{x^{2k}}{(2k)!} = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \frac{x^6}{6!} + \cdots$$

$$\sin x = \sum_{k=0}^\infty (-1)^k \frac{x^{2k+1}}{(2k+1)!} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \cdots$$

$$\ln(1+x) = \sum_{n=1}^\infty (-1)^{n+1} \frac{x^n}{n} = x - \frac{x^2}{2} + \frac{x^3}{3} - \frac{x^4}{4} + \cdots$$

$$\tan^{-1} x = \sum_{k=0}^\infty (-1)^k \frac{x^{2k+1}}{2k+1} = x - \frac{x^3}{3} + \frac{x^5}{5} - \frac{x^7}{7} + \cdots$$

$$(1+x)^a = 1 + \frac{a}{1!}x + \frac{a(a-1)}{2!}x^2 + \frac{a(a-1)(a-2)}{3!}x^3 + \cdots$$

### Operations on Series

Within the radius of convergence, series can be added, multiplied, differentiated, and integrated term-by-term. For example, integrating the geometric series for $1/(1+u)$ gives the series for $\ln(1+x)$. Differentiating gives the series for $1/(1-x)^2$.

### Taylor Series with Base Point $b$

$$f(x) = f(b) + f'(b)(x-b) + \frac{f''(b)}{2}(x-b)^2 + \frac{f^{(3)}(b)}{3!}(x-b)^3 + \cdots$$

For $\sqrt{x}$, use base point $b=1$ rather than $b=0$ (where the function is not differentiable).

## Weighted Averages

The weighted average of $f$ with weighting function $w$:

$$\text{Average}(f) = \frac{\int_a^b w(x)f(x)\,dx}{\int_a^b w(x)\,dx}$$

### Application: Annuity

The expected payout of an annuity with decay rate $e^{-kt}$ and payout $f(t) = t$ is:

$$\text{Expected payout} = \frac{\int_0^\infty t e^{-kt}\,dt}{\int_0^\infty e^{-kt}\,dt} = \frac{1}{k} = \frac{H}{\ln 2}$$

where $H$ is the half-life (or life expectancy in the case of a human).

## See Also

- [MIT 18.01 Unit 3: The Definite Integral](mit-18.01-unit3-definite-integrals.md) — fundamental theorem of calculus and basic integration, prerequisite to this unit
- [MIT 18.01 Unit 2: Applications of Differentiation](mit-18.01-unit2-applications-of-differentiation.md) — antiderivatives and separation of variables
- [MIT 18.01 Unit 1: Derivatives](mit-18.01-unit1-derivatives.md) — prerequisite material on differentiation
