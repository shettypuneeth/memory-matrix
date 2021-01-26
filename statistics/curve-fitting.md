# Curve fitting

## Least square method

Using the LSQ method we'll try to fit a collection of points (x, y) into a straight line.

Equation for a line:

> f(x) = mx + c

Least square fit aims to minimize the error in approximating `y` for by finding the right values for `m` and `c`.

The error in computation is represented aims

`E = sqrt(1/n * sum[1:n](square(f(Xk) - Yk)))`

Reduced to essentially:

`sum[1:n](square(m * Xk + c - Yk))`

Whenever we talk about finding minimum, we are in the realm of calculus as a derivative is essentially indicative of a minima or maxima with respect to varying values.

In our case, collection of (x, y) is given to us, only variables are `m` and `c`.
So we need to arrive at

`dE/dm = 0` and `dE/dc = 0`

`dE/dm => sum[1:n](2 * (mXk + c - Yk) * Xk) = 0`

`dE/dc => sum[1:n](2 * (mXk + c - Yk) * 1) = 0`

Focussing just on `dE/dm`
`Σ[1:n](mXk² + Xk * c - XkYk) = 0`

This comes down to solving a linear system AX = B

[ΣXk² ΣXk][m] = [ΣXkYk]
[ΣXk    n][c] = [ΣYk]