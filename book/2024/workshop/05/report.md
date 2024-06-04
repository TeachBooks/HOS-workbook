# Component Reliability Analysis Report

**Due date:** make your last commit before 4am on Tuesday, May 28, 2024. Contact Robert if you can't make the deadline.

The instructions are the same as for WS02; [Unit Website](https://tudelft-citg.github.io/HOS-prob-design-24/info/#grading).

**If your group has changed from WS02, email Robert an updated list of your group members.**

_This `Report.md` is set up in a format that illustrates essential information to report whenever you complete a component reliability analysis. Keep this in mind when doing this in the future._

**Question 1:** Describe the repository and code used to complete the analysis.

_Note: this answer has already been filled in for you!_

This repository contains all code needed to complete the component reliability analysis, which requires use of the finite element method (FEM). The code has been broken down into two parts, associated with the deterministic and probabilistic parts of the analysis:

- Deterministic:
  - The limit-state function uses a custom FEM code to solve for stresses in the element, located in sub-directory `stresses`
  - Notebook `Analysis_deterministic.ipynb` illustrates the use of this code.
- Probabilistic:
  - The Python package OpenTURNs is used for Monte Carlo and FORM analyses, which are defined in sub-directory `reliability`.
  - Notebook `Analysis_reliability.ipynb` illustrates the use of this code and performs the reliability analysis including results described in this report).
- All required packages are listed in `requirements.txt`.

**Question 2:** Describe the random variables and the multivariate distribution. 

_Note: this answer has already been filled in for you!_

Three hydrodynamic effects were considered as random variables in this problem, as they have the greatest uncertainty and the largest impact on the stresses in the tunnel elements. Marginal distributions are defined in the table below. All random variables are assumed to be independent; therefore they are implemented in OpenTURNs using a Multivariate Gaussian distribution (`NormalCopula`) with an identity matrix to define the correlation structure. Only one of the compressive strenght variables was used at a time.

| Symbol | Code | Description | Units | Distribution | Parameter(s) | OpenTURNs Implementation |
| :---: | :---: | :--- | :---: | :---: | :---: | :---: |
| $H^{1/3}$ | `X1` | Significant wave height, swell waves | m |  Exponential | 2.0309 | `Exponential(2.0309)` |
| $H^{1/3}$ | `X2` | Significant wave height, wind sea waves | m | Exponential | 2.0663 | `Exponential(2.0663)` |
| $u$ | `X3` | Velocity of current | m/s | Normal | 2, 0.2 | `Normal(2, 0.2)` |
| $\sigma_c$ | `X4` | Compressive strength of concrete | MPa | Normal | 75, 5 | `Normal(75, 5)` |
| $\sigma_s$ | `X4` | Compressive strength of steel | MPa | Normal | 250, 20 | `Normal(250, 20)` |

**Question 3:** Describe the limit-state function.

_Hint: key ingredients 3 and 4. Include a brief description of failure, the equation, as well as how it was implemented in the function `myLSF`. You should explicitly state how the LSF if formulated based on the results of the stress analysis using FEM._ 

_Your answer here._

Failure occurs when stress at any location in the tunnel element exceeds the maximum allowable stress of the concrete.

$$
g_X(x)=\sigma_{\textrm{max allowable}} - \sigma_{\textrm{max in tunnel element}}
$$

The FEM analysis compute stress at every element in the mesh; since we are interested in the maximum value, the limit-state function is formulated such that it finds the maximum value of all stress computations for all elements. Since the stress can have a positive or negative value (compression or tension), the absolute value is taken. The implementation in Python is thus:

```
myLSF = max_allowable_stress - np.max(stress_in_all_elements)
```

_Note this is not the actual code, but a pseudo-code representation._

**Question 4:** Describe the reliability algorithms used.

_Include a brief statement about the complexity of the stress analysis (i.e., computation time) and how that influenced your choice of reliability method. Do not include long descriptions of each method, but rather state the name and why you used it._

_Your answer here._

FEM takes 2.5 seconds to run. Since we will probably need at least 1000 simulations to compute a probability of 1%, the calculation time will be on the order of 30 minutes. This means MCS is not practical, so we should try using FORM, which converges more quickly. In the end form takes around 3 minutes, so it is an order of magnitude faster.

**Question 5:** present the main quantitative results and comment on their relevance to the design problem of interest. Report also how long it took to run each analysis.

_Include $p_f$, $\beta$, $x^*$, importance factors, along with any observations you may have._

_Your answer here._

Present quantitative values. Comment on loads/resistances, and state which variables have the biggest impact.

| Case | $p_f$ | Run Time |
| :---: | :---: | :---: |
| Hyraulic random variables only (3) | 0.1845 |  3 min |
| Including strength as RV (concrete) | 0.1860 | 3 min | 
| Including strength as RV (concrete with reduced $\sigma$) | 0.1846 | 4 min | 
| Including strength as RV (steel) | 0.0006 | 7 min |

**Question 6:** what is your recommendation for tunnel material? Justify your answer with quantitative results from the deterministic and probabilistic notebooks.

_Your answer here._

As can be seen in the results above, the steel dramatically reduces the failure probability, much more than reducing the standard deviation. Use that! The deterministic results would have been sufficient to indicate that this would be the case (without including capacity as a random variable), as it is clear the stress along the tunnel alignment exceeds 75 for a significant portion of its length.

**Question 7:** you will be expected to include a component reliability analysis in your B Module projects/exercises later in the quarter in a similar way to this workshop. This question is a chance to let us know if you do not yet feel comfortable doing that. Use the space below to let us know if you have any questions or suggestions for what we could do to make sure this goes smoothly for you.

_An answer to this question is optional._
