# Overview

```{note}
Remember, the concept of _component reliability analysis_ is introduced in the textbook [here](https://teachbooks.tudelft.nl/risk-reliability/reliability-component/overview.html). The pages in this workbook provide additional information to help you through the exercises and workshop assignments related to this material.
```

There are several key ingredients needed for a component reliability analysis:
1. Random variables, $X$, each of which has a marginal distribution
2. A multivariate probability distribution, $f_X(x)$
4. A function that takes the random variables as inputs and describes the performance of the _component_ of interest, $q_X(x)$ (i.e., a _function of random variables_)
5. A criteria that describes a "region of interest," a subset of the random variables, referred to as $\Omega$
6. An algorithm that solves for the probability of observing the conditions described by $\Omega$, defined by the following integral:

$$
P[\Omega] = \int_{\Omega} f_X(x) \; \mathrm{d} X
$$

In many civil engineering applications, we wish to evaluate failure probability (the inverse of reliability) of a particular object (i.e., the _component_). If we can formulate a function of random variables such that the output defines _failure_ of the component, then $P[\Omega]$ is the failure probability, $p_f$.

By convention, we prefer to write our function of random variables $q_X(x)$ such that values less than zero denote a failed condition; we also use the notation $g_X(x)$. The failure probability integral thus becomes:

$$
p_f = P[g_X(x)<0] = \int_{\Omega} f_X(x) \; \mathrm{d}X
$$

The equation $g_X(x)$ is called the _limit state function._

Note that if we can evaluate the distribution of $g_X(x)$ (denoted $f_g(x)$), then the integral is simply:

$$
p_f = P[g<0] = F_g(g=0) = \int_{-\infty}^{0} f_g(x) \; \mathrm{d}X
$$

In some cases this can be done analytically, but for most practical cases it is not possible.