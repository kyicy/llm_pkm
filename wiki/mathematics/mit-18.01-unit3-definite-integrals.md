# MIT 18.01 Single Variable Calculus — Unit 3: The Definite Integral and Its Applications

> Sources: MIT OpenCourseWare, Fall 2006
> Raw: [MIT 18.01 Unit 3 Definite Integrals](../../raw/learning/mit-18.01-unit3-definite-integrals.md)

## Overview

The third unit of MIT's 18.01 Single Variable Calculus (Fall 2006, taught by Professor David Jerison) introduces the definite integral as a limit of Riemann sums, establishes the Fundamental Theorem of Calculus connecting integration and differentiation, and applies integration to geometry (areas, volumes), physics (work, fluid flow), probability (normal distribution), and numerical approximation.

## The Definite Integral

The area under a curve $y = f(x)$ from $a$ to $b$ is defined as a limit of Riemann sums:

$$\int_a^b f(x)\,dx = \lim_{n \to \infty} \sum_{i=1}^n f(c_i)\,\Delta x, \quad \Delta x = \frac{b-a}{n}$$

where $c_i$ is any sample point in the $i$-th subinterval. This limit, when it exists, is the **definite integral**.

### Example: $f(x) = x^2$ on $[0, b]$

Dividing into $n$ intervals of width $b/n$ and using right endpoints:

$$\sum_{i=1}^n \left(\frac{ib}{n}\right)^2 \cdot \frac{b}{n} = \frac{b^3}{n^3}(1^2 + 2^2 + \cdots + n^2)$$

The sum of squares is bounded between $n^3/3$ and $(n+1)^3/3$, proved geometrically by comparing a staircase pyramid to inner and outer prisms. Taking the limit:

$$\int_0^b x^2\,dx = \frac{b^3}{3}$$

### Pattern

For $f(x) = x$, the area is $b^2/2$. For $f(x) = x^2$, the area is $b^3/3$. This suggests $\frac{d}{db}(\text{area}) = f(b)$, motivating the Fundamental Theorem.

## First Fundamental Theorem of Calculus (FTC 1)

If $f$ is continuous and $F'(x) = f(x)$, then:

$$\int_a^b f(x)\,dx = F(b) - F(a)$$

### Examples

- $\displaystyle\int_0^\pi \sin x\,dx = [-\cos x]_0^\pi = 2$ (area under one hump)
- $\displaystyle\int_0^{2\pi} \sin x\,dx = 0$ (positive and negative areas cancel)
- $\displaystyle\int_0^1 x^5\,dx = \frac{1}{6}$

### Properties of the Definite Integral

- **Additivity**: $\int_a^b f + \int_b^c f = \int_a^c f$
- **Reverse limits**: $\int_b^a f = -\int_a^b f$
- **Monotonicity**: If $f(x) \le g(x)$, then $\int_a^b f \le \int_a^b g$ (for $a < b$)

### Change of Variable (Substitution) for Definite Integrals

If $u = u(x)$ with $du = u'(x)dx$, then:

$$\int_{x_1}^{x_2} f(x)\,u'(x)\,dx = \int_{u_1}^{u_2} g(u)\,du, \quad u_i = u(x_i)$$

Example: $\int_1^2 (x^3 + 2)^4 x^2\,dx$. Let $u = x^3 + 2$, then $du = 3x^2 dx$:

$$\int_1^2 (x^3 + 2)^4 x^2\,dx = \int_3^{10} \frac{u^4}{3}\,du = \frac{10^5 - 3^5}{15}$$

## Second Fundamental Theorem of Calculus (FTC 2)

If $F(x) = \int_a^x f(t)\,dt$ and $f$ is continuous, then:

$$F'(x) = f(x)$$

This guarantees that every continuous function has an antiderivative (defined as an integral). It also provides a geometric proof: $\Delta F \approx f(x)\Delta x$, so $F'(x) = f(x)$.

### Proof of FTC 1 using FTC 2

Define $G(x) = \int_a^x f(t)\,dt$. By FTC 2, $G'(x) = f(x)$. If $F'(x) = f(x)$, then $(F - G)' = 0$, so $F - G$ is constant. Since $G(a) = 0$, we get $F(b) - F(a) = G(b) = \int_a^b f$.

### Functions Defined by Integrals

FTC 2 allows defining new functions via integrals:

- **Error function** (statistics): $\displaystyle\text{erf}(x) = \frac{2}{\sqrt{\pi}}\int_0^x e^{-t^2}\,dt$, with $\lim_{x\to\infty} \text{erf}(x) = 1$
- **Logarithmic integral** (number theory): $\displaystyle\text{Li}(x) = \int_2^x \frac{dt}{\ln t}$, approximating the count of primes less than $x$
- **Fresnel integrals** (optics): $\displaystyle C(x) = \int_0^x \cos(t^2)\,dt$, $\displaystyle S(x) = \int_0^x \sin(t^2)\,dt$
- **Bessel functions** (circular symmetry): $\displaystyle J_0(x) = \frac{1}{2\pi}\int_0^\pi \cos(x\sin\theta)\,d\theta$

## The Natural Logarithm via the Integral

Define $L(x) = \int_1^x \frac{dt}{t}$ for $x > 0$. By FTC 2:

$$L'(x) = \frac{1}{x}, \quad L(1) = 0$$

Key properties derived from this definition:

1. **Multiplication becomes addition**: $L(ab) = L(a) + L(b)$. Proof uses the substitution $t = au$.
2. **$L(x) \to \infty$ as $x \to \infty$**: $L(2^n) = nL(2) \to \infty$.
3. **$L(x) \to -\infty$ as $x \to 0^+$**: $L(x) = -L(1/x)$.

Thus $L(x)$ is the natural logarithm $\ln x$. This approach provides a cleaner foundation than the earlier method involving $a^x$ and $e$.

## Areas Between Curves

The area between two curves $y = f(x)$ (top) and $y = g(x)$ (bottom) from $a$ to $b$ is:

$$A = \int_a^b (f(x) - g(x))\,dx$$

### Example: $x = y^2$ and $y = x - 2$

The curves intersect at $(1, -1)$ and $(4, 2)$. Using **horizontal slices**:

$$A = \int_{-1}^2 ((y + 2) - y^2)\,dy = \frac{9}{2}$$

This is simpler than the vertical slice approach, which would require splitting the region at $x = 1$.

## Volumes of Revolution

### Method of Disks

Rotating $y = f(x)$ around the $x$-axis, a thin slice at $x$ has volume $dV = \pi y^2\,dx$.

**Example: Volume of a sphere of radius $a$.** Rotating $y = \sqrt{a^2 - x^2}$ around the $x$-axis:

$$V = \int_{-a}^a \pi(a^2 - x^2)\,dx = \frac{4}{3}\pi a^3$$

### Method of Shells (Cylinders)

Rotating around the $y$-axis, a thin cylindrical shell at radius $x$ has height $f(x)$, circumference $2\pi x$, thickness $dx$:

$$dV = 2\pi x f(x)\,dx$$

**Example: Witch's cauldron.** The region under $y = x^2$ rotated around the $y$-axis:

- **Disks** ($dy$): $V = \int_0^a \pi x^2\,dy = \int_0^a \pi y\,dy = \frac{\pi a^2}{2}$
- **Shells** ($dx$): $V = \int_0^{\sqrt{a}} (a - x^2)(2\pi x)\,dx = \frac{\pi a^2}{2}$

### Poiseuille Flow in a Pipe

Fluid velocity in a pipe of radius $R$ follows $v = c(R^2 - r^2)$. The total flow through an annular ring of radius $r$ and thickness $dr$ is:

$$\text{flow} = \int_0^R c(R^2 - r^2) \cdot 2\pi r\,dr = \frac{\pi}{2}cR^4$$

The $R^4$ dependence means doubling pipe radius increases flow by a factor of 16.

## Average Value

The average value of a continuous function $f$ on $[a, b]$ is:

$$\overline{f} = \frac{1}{b-a}\int_a^b f(x)\,dx$$

### Example: Average height of a semicircle

For $y = \sqrt{1 - x^2}$ on $[-1, 1]$:

$$\overline{y} = \frac{1}{2}\int_{-1}^1 \sqrt{1 - x^2}\,dx = \frac{\pi}{4}$$

### Weighted Averages

For the witch's cauldron with temperature $T(y) = 100 - 30y$, the average temperature weighted by volume (using disks of area $\pi y$) is:

$$\overline{T} = \frac{\int_0^1 T(y) \cdot \pi y\,dy}{\int_0^1 \pi y\,dy} = \frac{40\pi}{\pi/2} = 80^\circ\text{C}$$

This differs from the unweighted average ($85^\circ\text{C}$) because there is more water at cooler temperatures near the top.

## The Gaussian Integral

$$Q = \int_{-\infty}^\infty e^{-x^2}\,dx$$

This fundamental integral is computed by a clever trick using volumes of revolution:

1. Express $Q^2 = \int_{-\infty}^\infty e^{-x^2}\,dx \cdot \int_{-\infty}^\infty e^{-y^2}\,dy = \iint_{\mathbb{R}^2} e^{-(x^2+y^2)}\,dx\,dy$
2. Convert to polar coordinates (via the solid of revolution of $e^{-r^2}$):
   $$V = \int_0^\infty e^{-r^2} \cdot 2\pi r\,dr = \pi$$
3. But also $V = \int_{-\infty}^\infty A(y)\,dy$ where $A(y) = \int_{-\infty}^\infty e^{-(x^2+y^2)}\,dx = e^{-y^2}Q$
4. Hence $V = Q \int_{-\infty}^\infty e^{-y^2}\,dy = Q^2$, so $Q = \sqrt{\pi}$

This yields the normalization constant for the normal distribution:

$$\frac{1}{\sqrt{2\pi}\sigma} \int_{-\infty}^\infty e^{-x^2/2\sigma^2}\,dx = 1$$

## Numerical Integration

Three methods for approximating $\int_a^b f(x)\,dx$ when an antiderivative is unavailable:

### Riemann Sum (Left or Right Endpoint)

$$R_n = \Delta x \sum_{i=0}^{n-1} y_i \quad \text{or} \quad \Delta x \sum_{i=1}^n y_i, \quad \Delta x = \frac{b-a}{n}$$

### Trapezoidal Rule

Averages the left and right Riemann sums, giving:

$$T_n = \Delta x\left(\frac{y_0}{2} + y_1 + y_2 + \cdots + y_{n-1} + \frac{y_n}{2}\right)$$

### Simpson's Rule

Approximates the function by quadratics over pairs of intervals ($n$ must be even):

$$\int_a^b f(x)\,dx \approx \frac{\Delta x}{3}(y_0 + 4y_1 + 2y_2 + 4y_3 + 2y_4 + \cdots + 4y_{n-1} + y_n)$$

Coefficient pattern: $1, 4, 2, 4, 2, \ldots, 2, 4, 1$. Simpson's rule is significantly more accurate than the trapezoidal rule — its error is $O((\Delta x)^4)$.

### Example: $\int_0^1 \frac{dx}{1+x^2}$

With $n=2$ ($\Delta x = 1/2$):

- Trapezoidal: $0.775$ (error $\approx 0.010$)
- Simpson's: $0.78333$ (error $\approx 0.002$)
- Exact: $\pi/4 \approx 0.785$

## Work

Work is force times distance. When the force varies, integrate:

$$W = \int F\,ds$$

### Example: Pendulum

A pendulum of length $L$ with mass $m$ at angle $\theta$. The tangential component of gravity is $mg\sin\theta$, and the arc length element is $L\,d\theta$:

$$W = \int_0^{\theta_0} (mg\sin\theta)(L\,d\theta) = Lmg(1 - \cos\theta_0)$$

This equals $mg$ times the vertical drop $L(1 - \cos\theta_0)$, confirming that work depends only on change in height, not the path taken — there is no perpetual motion machine.

## See Also

- [MIT 18.01 Unit 1: Derivatives](mit-18.01-unit1-derivatives.md) — prerequisite material on differentiation
- [MIT 18.01 Unit 2: Applications of Differentiation](mit-18.01-unit2-applications-of-differentiation.md) — antiderivatives and separation of variables, continued in this unit
- [MIT 18.01 Unit 4: Techniques of Integration and Series](mit-18.01-unit4-integration-and-series.md) — completes the course with advanced integration methods, polar coordinates, and Taylor series
