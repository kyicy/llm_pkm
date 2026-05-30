# MIT 18.01 Single Variable Calculus — Unit 1: Derivatives

> Sources: MIT OpenCourseWare, Fall 2006
> Raw: [MIT 18.01 Unit 1 Derivatives](../../raw/learning/mit-18.01-unit1-derivatives.md)

## Overview

A comprehensive overview of the first unit of MIT's 18.01 Single Variable Calculus (Fall 2006), covering the definition and computation of derivatives, limits and continuity, trigonometric limits, differentiation rules (product, quotient, chain rule), implicit differentiation, derivatives of exponentials and logarithms, and hyperbolic functions. The course is taught by Professor David Jerison.

## Geometric Interpretation of the Derivative

The derivative $f'(x_0)$ is the slope of the line tangent to the graph of $f$ at the point $(x_0, f(x_0))$. Formally, it is the limit of slopes of secant lines as the two points coalesce:

$$f'(x_0) = \lim_{\Delta x \to 0} \frac{f(x_0 + \Delta x) - f(x_0)}{\Delta x}$$

This "difference quotient" always requires algebraic cancellation — plugging $\Delta x = 0$ directly yields $0/0$.

### Example: $f(x) = 1/x$

$$f'(x_0) = -\frac{1}{x_0^2}$$

This derivative is negative everywhere (the function is decreasing). The tangent line at any point on this hyperbola forms a triangle with the coordinate axes whose area is always $2$.

### Notations for the Derivative

- Leibniz: $\dfrac{dy}{dx}$
- Newton: $f'(x_0)$
- Other: $\dfrac{df}{dx}$, $\dot{f}$, $Df$

## Derivatives of Power Functions

For $f(x) = x^n$ ($n = 1, 2, 3, \dots$):

$$\frac{d}{dx}(x^n) = nx^{n-1}$$

Derived using the binomial theorem expansion $(x + \Delta x)^n = x^n + n(\Delta x)x^{n-1} + O\!\left((\Delta x)^2\right)$. Extends to polynomials term-by-term.

## Limits and Continuity

A function $f$ is continuous at $x_0$ when $\displaystyle\lim_{x \to x_0} f(x) = f(x_0)$. Four types of discontinuity:

1. **Removable** — left and right limits equal but not equal to $f(x_0)$
2. **Jump** — left and right limits exist but differ
3. **Infinite** — limits diverge to $\pm\infty$ (e.g., $1/x$ at $x = 0$)
4. **Ugly** — oscillatory behavior, limit does not exist

**Key theorem:** Differentiability implies continuity (but not vice versa).

### Trigonometric Limits ($\theta$ in radians)

$$\lim_{\theta \to 0} \frac{\sin\theta}{\theta} = 1 \qquad \lim_{\theta \to 0} \frac{1 - \cos\theta}{\theta} = 0$$

## Differentiation Rules

### Basic Rules

- $(u + v)' = u' + v'$
- $(cu)' = cu'$ ($c$ constant)

### Product Rule

$$(uv)' = u'v + uv'$$

Proof: Adding $u(x + \Delta x)v(x) - u(x + \Delta x)v(x) = 0$ to the numerator of the difference quotient, then rearranging and taking limits.

### Quotient Rule

$$\left(\frac{u}{v}\right)' = \frac{u'v - uv'}{v^2}$$

Can be derived from product rule by rewriting $u/v = u \cdot v^{-1}$.

### Chain Rule

$$\frac{dy}{dt} = \frac{dy}{dx}\frac{dx}{dt} \quad\text{or}\quad \frac{d}{dx}f(g(x)) = f'(g(x))\,g'(x)$$

Composition is not commutative: $f \circ g \neq g \circ f$.

### Derivatives of Trigonometric Functions

- $\dfrac{d}{dx}\sin x = \cos x$
- $\dfrac{d}{dx}\cos x = -\sin x$
- $\dfrac{d}{dx}\sec x = \tan x \sec x$
- $\dfrac{d}{dx}\arctan x = \dfrac{1}{1 + x^2}$

## Implicit Differentiation

When $y$ cannot be easily isolated, differentiate both sides of the equation with respect to $x$ (using the chain rule for $y$-terms) and solve for $\dfrac{dy}{dx}$.

### Example: $x^2 + y^2 = 1$

$$2x + 2y\frac{dy}{dx} = 0 \quad\Rightarrow\quad \frac{dy}{dx} = -\frac{x}{y}$$

### Example: $y^3 + xy^2 + 1 = 0$

$$3y^2\frac{dy}{dx} + y^2 + 2xy\frac{dy}{dx} = 0 \quad\Rightarrow\quad \frac{dy}{dx} = \frac{-y^2}{3y^2 + 2xy}$$

## Higher Derivatives

Higher derivatives are derivatives of derivatives. Notations:

- $f^{(n)}(x)$, $D^n f$, $\dfrac{d^n f}{dx^n}$

$$D^n x^n = n!$$

Proof by induction.

## Exponentials and Logarithms

### The Number $e$

Defined as the unique base such that $M(e) = 1$, where $\displaystyle M(a) = \lim_{\Delta x \to 0} \frac{a^{\Delta x} - 1}{\Delta x}$. Equivalently:

$$\frac{d}{dx}(e^x) = e^x$$

### Derivatives

- $\displaystyle\frac{d}{dx}(\ln x) = \frac{1}{x}$
- $\displaystyle\frac{d}{dx}(a^x) = \ln a \cdot a^x$
- $\displaystyle\frac{d}{dx}(x^r) = r x^{r-1}$ (for any real $r$)

### Logarithmic Differentiation

$$(\ln f)' = \frac{f'}{f} \quad\Rightarrow\quad f' = f \cdot (\ln f)'$$

Useful for functions with variable exponents. Example: $\displaystyle\frac{d}{dx}(x^x) = x^x(\ln x + 1)$.

### Key Limit

$$\lim_{k \to \infty} \left(1 + \frac{1}{k}\right)^k = e$$

## Hyperbolic Functions

- $\displaystyle\sinh x = \frac{e^x - e^{-x}}{2}$, $\displaystyle\frac{d}{dx}\sinh x = \cosh x$
- $\displaystyle\cosh x = \frac{e^x + e^{-x}}{2}$, $\displaystyle\frac{d}{dx}\cosh x = \sinh x$

**Identity:** $\cosh^2 x - \sinh^2 x = 1$ (analogous to $\cos^2 x + \sin^2 x = 1$ for circles, but describing a hyperbola).

## Physical Interpretation

The derivative represents an instantaneous rate of change. Examples:

- $\dfrac{dq}{dt} =$ electrical current (charge flow)
- $\dfrac{ds}{dt} =$ speed (distance traveled)
- $\dfrac{dT}{dx} =$ temperature gradient
- Pumpkin drop: $y = 400 - 16t^2$ $\to$ velocity $y' = -32t$

The derivative appears wherever measurement involves change: physics, economics, finance, engineering, and GPS sensitivity analysis.

## See Also

- [MIT 18.01 Unit 2: Applications of Differentiation](mit-18.01-unit2-applications-of-differentiation.md) — linear/quadratic approximations, curve sketching, optimization, related rates, and differential equations
- [MIT 18.01 Unit 3: The Definite Integral](mit-18.01-unit3-definite-integrals.md) — continues with Riemann sums, FTC, volumes, and applications of integration
- [MIT 18.01 Unit 4: Techniques of Integration and Series](mit-18.01-unit4-integration-and-series.md) — completes the series with advanced integration methods, polar coordinates, and Taylor series
- [Feynman Technique](../learning/feynman-technique.md) — study methods applicable to learning calculus
