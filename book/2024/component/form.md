# First-Order Reliability Method (FORM)

This page gives an overview of the First-Order Reliability Method (FORM). It is an algorithm for solving the component reliability problem, which was first applied during Workshop 04. Once reading through this page, it may be useful to refer back to the solution for WS04, especially the graphical interpretation in the notebook.

## A Linearized Solution

The "FO" part of the algorithm name stands for "First Order" because the method is based on a linearized approximation (using a Taylor Series) of the limit-state function. This can be visualized in the figure below, where the 

```{image} ../figures/form_x.jpg
:alt: form in x space
:width: 300px
:align: center
```

The contours illustrated in the figure are probability density. It is essential to recognize that the probability of interest (i.e., failure probability) is the volume underneath the shaded area and is found by integrating the probability density in the region of interest.

## Design Point

The design point is simply the expansion point of Taylor's Series used in the linear approximation, of which there are infinite possible choices to select from. However, the FORM method uses a particular definition of the design point (also referred to as the Hasofer-Lind design point, after those who proposed it).

Specifically, the design point, $x^*$, is:

1. A point on the limit-state surface such that $g_X(x^*)=0$
2. Of all the points on the limit-state surface, it is that which maximizes probability density $f_X(x^*)$

This is chosen for several reasons, the most important being that it produces a linearized limit-state function that will give the most suitable approximation of the failure probability, as well as producing insight into the problem of interest (i.e., the design variables and how they relate to the failure probability).

It is interesting to note that the design point also represents the shortest distance between the mean point of the probability density function and the limit-state surface. This will have a particularly important result when we transform the computations to the standard normal space, in the next section.

FORM is simply an algorithm that efficiently searches for the design point. It can be implemented with many optimization algorithms (e.g., in OpenTURNs we will use the `Cobyla` method).

## Computations in Standard Normal Space

Although we do not cover the approach here, the FORM calculations are actually being performed in the standard normal space. This makes the computations more feasible (we can use relatively simple distributions) as well as numerically more efficient. All random variables (including their multivariate distribution and the limit-state function) have been transformed to those with the Normal distribution of zero mean and variance of 1. The variables are also uncorrelated. This results in contours of probability density that are concentric circles, as illustrated in the figure below.

```{image} ../figures/form_u.jpg
:alt: form in u space
:width: 300px
:align: center
```

Note also that the distance between the mean point (origin) and the design point in the standard normal space ($u^*$) is the shortest distance to the limit-state surface. Because the limit-state is linearized, this distance is a normal vector (i.e., it is perpendicular). 

Although this may seem like a strange approach, you have probably used the transformation before: it is in fact what you are doing when using a standard probability table for the Normal distribution! Typically, you convert the value of your random variable, $X$, to another variable $Z$, such that:

$$
z=\frac{x-\mu_X}{\sigma_X}
$$

And the probability of $Z$, the CDF $F_Z(z)$, is found in the table. The key point here, relative to FORM, is that we performed the probability computation in the standard normal space (the $Z$ variable). As illustrated in the figure above, we are using $U$ to represent the multivariate standard normal variables.

## Computing the Probability of Failure

An interesting property of the standard normal space is that the mean of all random variables is at the origin, and the shortest distance to the limit-state surface is tangent to the linearized function. This distance, defined here as $\beta$, makes the computation of failure probability straightforward using the CDF of the standard normal multivariate distribution, $\Phi$:

$$
p_f = \Phi [-\beta]
$$

Although this may seem complicated (due to the multivariate aspect), it is in fact no different than what you have done previously in the 1D standard normal case. Consider the figure below, which illustrates $\beta$ as the "distance" between the mean and the point of interest (where we want to start our integral):

```{image} ./figures/beta_1d.jpg
:alt: beta in 1d
:width: 300px
:align: center
```

From linear algebra, we can show that the distance, can be computed as the vector product:

$$
\beta = \alpha u^*
$$

Where $\alpha$ is a unit vector normal to the linearized limit state function:

$$
\alpha = -\frac{\nabla g_U(u^*)}{||\nabla g_U(u^*)||}
$$

## Importance Factors, $\alpha$

The derivation of $\alpha$ is outside the scope of our work, but it is important to recognize that it is found from the gradient of the limit-state function, which means it is

## Essential Results of a FORM Analysis

