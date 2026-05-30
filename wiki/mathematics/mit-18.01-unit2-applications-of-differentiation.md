# MIT 18.01 Single Variable Calculus — Unit 2: Applications of Differentiation

> Sources: MIT OpenCourseWare, Fall 2006
> Raw: [MIT 18.01 Unit 2 Applications of Differentiation](../../raw/learning/mit-18.01-unit2-applications-of-differentiation.md)

## Overview

The second unit of MIT's 18.01 Single Variable Calculus (Fall 2006, taught by Professor David Jerison) applies differentiation to a wide range of problems: approximating functions near a point, sketching curves, optimizing quantities, solving related rates problems, finding roots of equations, establishing inequalities, and solving elementary differential equations. The central theme is that knowledge of $f'$ (and sometimes $f''$) reveals properties of $f$ itself.

## Linear Approximation

For a differentiable function $f$ near a basepoint $x_0$, the tangent line provides a first-order approximation:

$$f(x) \approx f(x_0) + f'(x_0)(x - x_0)$$

This is accurate near $x_0$ but degrades as one moves away. A convenient choice is $x_0 = 0$, giving the basic linear approximations for $|x| \ll 1$:

1. $\sin x \approx x$
2. $\cos x \approx 1$
3. $e^x \approx 1 + x$
4. $\ln(1 + x) \approx x$
5. $(1 + x)^r \approx 1 + rx$

Approximations can be combined algebraically. For example, $f(x) = e^{-2x} / \sqrt{1 + x}$ near $x = 0$:

$$e^{-2x} \approx 1 - 2x, \quad \sqrt{1 + x} \approx 1 + \frac{1}{2}x, \quad \frac{e^{-2x}}{\sqrt{1 + x}} \approx 1 - \frac{5}{2}x$$

### Application: Time Dilation

From special relativity, $T' = T / \sqrt{1 - v^2/c^2}$. Using $(1 + u)^{-1/2} \approx 1 - u/2$, we get:

$$T' \approx T\left(1 + \frac{v^2}{2c^2}\right)$$

For GPS satellites ($v = 4$ km/s, $c = 3 \times 10^5$ km/s), $v^2/c^2 \approx 10^{-10}$, so the correction is tiny but measurable — engineers use it to calibrate satellite transmitter frequencies.

## Quadratic Approximation

When higher accuracy is needed, include the second derivative term:

$$f(x) \approx f(x_0) + f'(x_0)(x - x_0) + \frac{f''(x_0)}{2}(x - x_0)^2$$

The factor of $1/2$ ensures the approximation is exact for quadratic functions $f(x) = a + bx + cx^2$. Basic quadratic approximations at $x_0 = 0$:

1. $\sin x \approx x$
2. $\cos x \approx 1 - \dfrac{x^2}{2}$
3. $e^x \approx 1 + x + \dfrac{x^2}{2}$
4. $\ln(1 + x) \approx x - \dfrac{x^2}{2}$
5. $(1 + x)^r \approx 1 + rx + \dfrac{r(r-1)}{2}x^2$

In practice, the quadratic term is often negligible. For the time dilation example, the quadratic term is on the order of $10^{-20}$, far below atomic clock precision.

## Curve Sketching

The signs of $f'$ and $f''$ determine a function's shape. The rubric for sketching $y = f(x)$:

1. Plot discontinuities — especially infinite ones.
2. Find critical points where $f'(x) = 0$.
3. Plot critical points (if easy); determine the sign of $f'$ between them.
4. Find zeros of $f$ (if easy).
5. Determine endpoint behavior (including $\pm\infty$).

### Key Example: $y = 3x - x^3$

- $y' = 3 - 3x^2 = 0$ at $x = \pm 1$; critical values: $(1, 2)$ and $(-1, -2)$.
- Zeros at $x = 0, \pm\sqrt{3}$.
- As $x \to \infty$, $y \to -\infty$; as $x \to -\infty$, $y \to \infty$.

### Warning: Discontinuities

For $y = 1/x$, $y' = -1/x^2 < 0$ everywhere except $x = 0$, but the function is not decreasing across the discontinuity — it jumps from $-\infty$ to $+\infty$ at $x = 0$. Always check discontinuities before analyzing derivative sign.

### Second Derivative Information

- $f'' > 0$: $f$ is convex (concave up); $f'$ is increasing.
- $f'' < 0$: $f$ is concave down; $f'$ is decreasing.
- $f''(x_0) = 0$: inflection point (graph changes concavity).

**Second Derivative Test**: At a critical point $x_0$ where $f'(x_0) = 0$:
- $f''(x_0) > 0$: local minimum.
- $f''(x_0) < 0$: local maximum.

## Max/Min Problems

Strategy for optimization:

1. Draw a picture and name variables.
2. Identify constraints and express them as equations.
3. Express the quantity to optimize in a single variable.
4. Find critical points ($dS/dr = 0$, etc.) and endpoints.
5. Compare candidate values.

### Example: Open-Topped Can

Minimize surface area $S = \pi r^2 + 2\pi r h$ for fixed volume $V = \pi r^2 h$.

$$h = \frac{V}{\pi r^2}, \quad S = \pi r^2 + \frac{2V}{r}$$

$$S' = 2\pi r - \frac{2V}{r^2} = 0 \implies r = \left(\frac{V}{\pi}\right)^{1/3}$$

At this critical point, $h = r = (V/\pi)^{1/3}$, so the optimal can has height equal to radius. As $r \to 0$ or $r \to \infty$, $S \to \infty$, confirming this is a minimum.

### Example: Wire Cut into Squares

A wire of length 1 is cut at $x$, with each piece bent into a square. Total area:

$$A = \left(\frac{x}{4}\right)^2 + \left(\frac{1 - x}{4}\right)^2, \quad A' = 0 \implies x = \frac{1}{2}$$

This gives $A = 1/32$ — a minimum. The maximum area ($1/16$) occurs at the endpoints $x = 0$ or $x = 1$ (using the whole wire for one square). **Always check endpoints.**

## Related Rates

Problems where quantities change over time and are linked by geometric or physical constraints.

General strategy:
1. Draw a picture. Set up variables and equations.
2. Differentiate implicitly with respect to time.
3. Plug in given numerical values *after* differentiating.

### Example: Radar Gun

Police are 30 feet from the road. Radar reads $D' = -80$ ft/s when $D = 50$ ft.

$$30^2 + x^2 = D^2 \implies 2xx' = 2DD' \implies x' = \frac{D}{x}D'$$

At $D = 50$, $x = 40$ (3-4-5 triangle), so $x' = (50/40)(-80) = -100$ ft/s, exceeding the speed limit of 95 ft/s.

### Example: Conical Tank

A conical tank (radius 4 ft at top, height 10 ft) fills at 2 ft³/min. Find how fast the water level rises when $h = 5$ ft.

Using similar triangles, $r/h = 4/10 = 2/5$, so $V = \frac{1}{3}\pi r^2 h = \frac{4}{75}\pi h^3$.

$$\frac{dV}{dt} = \frac{4}{25}\pi h^2 h' \implies 2 = \frac{4}{25}\pi(5)^2 h' \implies h' = \frac{1}{2\pi} \text{ ft/min}$$

## Newton's Method

A numerical method for solving $f(x) = 0$ by iterating:

$$x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}$$

### Example: $\sqrt{3}$

For $f(x) = x^2 - 3$, $f'(x) = 2x$, the iteration is $x_{k+1} = \frac{1}{2}\left(x_k + \frac{3}{x_k}\right)$.

Starting from $x_0 = 1$, the approximations converge rapidly:

| $x_0$ | 1 |
| $x_1$ | 2 |
| $x_2$ | 7/4 |
| $x_3$ | 7/4 + 6/7 |
| $x_4$ | 18817/10864 |

The number of accurate digits roughly doubles each iteration.

**Warnings:**
- The method can converge to an unexpected root (e.g., starting at $x_0 = -1$ converges to $-\sqrt{3}$).
- The method can fail entirely, cycling between two values rather than converging.

## Ring on a String

A ring slides freely on a string of fixed length $L$ anchored at $(0,0)$ and $(a,b)$. The ring settles at the lowest possible height (minimum potential energy). The constraint curve is an ellipse with foci at the anchor points.

At the critical point ($y' = 0$), implicit differentiation of the constraint yields $\sin\alpha = \sin\beta$, where $\alpha$ and $\beta$ are the angles the string makes with the vertical. Thus $\alpha = \beta$, a physical equilibrium condition (equal tension in both halves). Equivalently, the ellipse has the reflection property: a ray from one focus reflects to the other.

The coordinates of the lowest point are:

$$x = \frac{a}{2}\left(1 - \frac{b}{\sqrt{L^2 - a^2}}\right), \qquad y = \frac{1}{2}\left(b - \sqrt{L^2 - a^2}\right)$$

## Mean Value Theorem

If $f$ is differentiable on $a < x < b$ and continuous on $a \le x \le b$, then there exists $c$ with $a < c < b$ such that:

$$\frac{f(b) - f(a)}{b - a} = f'(c)$$

Equivalently, $f(b) = f(a) + f'(c)(b - a)$. This is an exact formula (unlike linear approximation which uses the definite slope $f'(a)$). It is the theoretical foundation of calculus.

### Key Consequences

1. If $f'(x) > 0$ for all $x$, then $f$ is strictly increasing.
2. If $f'(x) < 0$ for all $x$, then $f$ is strictly decreasing.
3. If $f'(x) = 0$ for all $x$, then $f$ is constant.

These non-obvious results justify the use of derivative sign analysis in curve sketching and optimization.

### Inequalities via MVT

The MVT can establish inequalities. For example, $e^x > 1 + x$ for $x > 0$:

- Let $f_1(x) = e^x - 1$. Since $f_1(0) = 0$ and $f_1'(x) = e^x > 0$, $f_1$ is increasing, so $e^x > 1$ for $x > 0$.
- Let $f_2(x) = e^x - (1 + x)$. Since $f_2'(x) = e^x - 1 = f_1(x) > 0$ for $x > 0$, $f_2$ is increasing, and $f_2(0) = 0$, so $e^x > 1 + x$ for $x > 0$.

By induction, $e^x > 1 + x + x^2/2 + \cdots + x^n/n!$, leading to the Taylor series.

## Differentials

Notation: $dy = f'(x)dx$. Both $dy$ and $f'(x)dx$ are called differentials. The derivative $dy/dx = f'(x)$ can be treated as a quotient of differentials.

### Example: $65^{1/3}$

With $y = x^{1/3}$ and base point $a = 64$:

$$dy = \frac{1}{3}x^{-2/3}dx \implies dy = \frac{1}{48}dx \quad \text{at } x = 64$$

Taking $dx = 1$ gives $65^{1/3} \approx 4 + 1/48$.

## Antiderivatives

$F(x) = \int f(x)\,dx$ means $F'(x) = f(x)$. Basic antiderivatives:

1. $\displaystyle\int \sin x\,dx = -\cos x + C$
2. $\displaystyle\int x^n\,dx = \frac{x^{n+1}}{n+1} + C$ ($n \neq -1$)
3. $\displaystyle\int \frac{dx}{x} = \ln|x| + C$ (covers $n = -1$)
4. $\displaystyle\int \sec^2 x\,dx = \tan x + C$
5. $\displaystyle\int \frac{dx}{\sqrt{1 - x^2}} = \sin^{-1} x + C$
6. $\displaystyle\int \frac{dx}{1 + x^2} = \tan^{-1} x + C$

**Uniqueness**: Antiderivatives are unique up to an additive constant. If $F' = G'$, then $G(x) = F(x) + C$.

### Substitution Method

Change variables to simplify the integral. Examples:

- $\displaystyle\int x^3(x^4 + 2)^5\,dx$: let $u = x^4 + 2$, $du = 4x^3\,dx$, yields $\frac{1}{24}(x^4 + 2)^6 + C$.
- $\displaystyle\int \frac{dx}{x\ln x}$: let $u = \ln x$, $du = dx/x$, yields $\ln(\ln x) + C$.

### Advanced Guessing

For $\int xe^{-x^2}\,dx$, guess $e^{-x^2}$. Check: $\frac{d}{dx}e^{-x^2} = -2xe^{-x^2}$, so $\int xe^{-x^2}\,dx = -\frac{1}{2}e^{-x^2} + C$.

## Separation of Variables

For ordinary differential equations of the form $dy/dx = f(x)g(y)$, separate variables:

$$\frac{dy}{g(y)} = f(x)\,dx \quad\implies\quad \int h(y)\,dy = \int f(x)\,dx \quad\text{where}\quad h(y) = \frac{1}{g(y)}$$

### Example: $dy/dx = -xy$

$$\frac{dy}{y} = -x\,dx \implies \ln|y| = -\frac{x^2}{2} + C \implies y = ae^{-x^2/2}$$

The constant $a = \pm e^C$ includes the case $a = 0$, corresponding to different initial conditions.

### Example: $dy/dx = 2y/x$

$$\frac{dy}{y} = \frac{2dx}{x} \implies \ln|y| = 2\ln|x| + C \implies y = ax^2$$

### Orthogonal Trajectories

For curves perpendicular to the family $y = ax^2$, the slopes satisfy:

$$\frac{dy}{dx} = -\frac{1}{\text{slope of parabola}} = -\frac{x}{2y}$$

Separating variables: $2y\,dy = -x\,dx \implies y^2 = -\frac{x^2}{2} + C$, which describes a family of ellipses.

## See Also

- [MIT 18.01 Unit 1: Derivatives](mit-18.01-unit1-derivatives.md) — prerequisite material covering limits, differentiation rules, and the definition of the derivative
- [MIT 18.01 Unit 3: The Definite Integral](mit-18.01-unit3-definite-integrals.md) — continues with Riemann sums, FTC, volumes, and applications of integration
- [MIT 18.01 Unit 4: Techniques of Integration and Series](mit-18.01-unit4-integration-and-series.md) — completes the series with advanced integration methods and infinite series
