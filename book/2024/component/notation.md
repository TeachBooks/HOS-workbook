# Notation

Multivariate probability density function (continuous random variables):

$$
f_X(x)
$$

where $X$ is a vector of $n$ random variables:

$$
X=[X_1, X_2, \ldots , X_n]
$$

realizations of a random variable $X_i$ are denoted with lower-case letters: $x_i$.

```{note} 
No distinction is made between a random vector (a vector of random variables) and a single random variables; both use notation $X$. You will have to use the context of the problem to determine which is the case (which should be obvious, if there is more than one random variable considered!).

```

## Functions of Random Variables

A generic function of interest will usually be represented with letter $q$:

$$
Q=q_X(x)
$$

where upper-case $Q$ implies that the output of the function is also a random variable (perhaps also a vectorized output). If the function $q_X$ includes non-random (deterministic) parameters, they will be denoted using $\theta$ to distinguish from random variables:

$$
Q=q_X(x,\theta)
$$

```{note}
Similar to random vectors, deterministic parameters may also be represented as vectors (this helps with linear algebra computations, for example, sensitivity calculation). For the case where $q$ has $m$ deterministic parameters:

$$
\theta = [\theta_1, \theta_2, \ldots, \theta_m]
$$
```

### Limit-State Function

The letter $g$ is used for the limit-state function; a special case of a function of random variables, $q$, formulated such that failure is explicitly defined as the situation $g_X(x)<0$.

$$
p_f = \int_\Omega g_X(x) \; \mathrm{d}X
$$

In this case, $\Omega$ is the failure region: the set of all $x$ such that the _component_ described by $q_X(x)$ and $g_X(x)$ fails. If $G$ is the random variable output of $g_X(x)$, then the failure probability can also be found as follows:

$$
p_f = P[g<0] = F_g(g=0) = \int_{-\infty}^{0} f_G(g) \; \mathrm{d}G
$$

Unfortunately the integral can rarely be evaluated directly due to $g_X(x)$ being a non-linear in $X$ and/or the distribution of $G$ being non-Gaussian.

```{note}
The use of capital $G$ here deviates from that of the Der Kiureghian textbook, where $G_U(u)$ is used to denote the limit-state function in the standard normal space (i.e., $g_U(u)$ in this book).
% RRRRR check ADK notation (also elsewhere on this page)
```

<!-- ### Parametric Distribution Parameters

In some cases it is useful to distinguish parameters of the function of random variables from the parameters of the continuous distribution functions using the subscripts -->