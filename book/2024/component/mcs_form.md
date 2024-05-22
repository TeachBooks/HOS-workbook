# Comparison of MCS and FORM

Monte Carlo Simulation (MCS) and the First-Order Reliability Method (FORM) are both algorithms used to solve the component reliability problem. Whereas the former is relatively straightforward and based on simulation (generating a set of random samples from the multivariate distribution), the latter involves a first-order approximation of the limit-state surface at an expansion point called the _design point_, $x^*$. There are pros and cons to each method, and in fact, _both_ methods can be used together when working on probabilistic design problems.

Note in particular for MCS:
- returns only the computed failure probability (ratio of failed realization to total number of samples)
- "solution" approach is very straightforward, and only requires evaluations of the function
- may require many evaluations of the limit-state function (typically $\sim$10 times the expected value of $1/p_f$, so around 10,000 simulations could be expected for probability of failure $0.001$)
- may be time-consuming if the function requires a long time to run (e.g., 10,000 simulations for a function that takes 1 minute to run will require nearly 7 days to finish!)

Note in particular for FORM:
- provides extra insight to the component reliability problem and the random variables via the design point, $x^*$ and importance factors, $\alpha$
- requires far fewer function evaluations than MCS (typically order 10-100 times the number of random variables)
- more complicated to implement and use, as it involves transformation of the random variables to the standard normal space and an optimization algorithm
- based on a linearized approximation of the limit-state function, so the computed probability is not "accurate," compared to MCS
- although dependence can be incorporated, the transformation to the standard normal space is also linearized, so insights should be considered local to the design point

In the end, it is good to use both methods together to optimize computation time while still allowing the iterative revise-evaluate-assess approach that is essential for design work. For example:

- use FORM to make many computations rapidly and explore the random variables and limit-state function
- use MCS to "check" that the failure probability computed by FORM is accurate (i.e., do the large simulation only once or twice, once you have a good idea of what the answer and final design should be)
- using the methods together can help resolve bugs in your code; for example, if FORM is "broken" you can run a small MCS to check that you have implemented everything correctly in OpenTURNs (e.g., the distributions or the limit-state function)