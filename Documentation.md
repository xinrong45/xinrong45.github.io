# Documentation


The purpose of this task is to calculate the optimal path on a Brownian sheet. Formulas for covariance and conditional expectation are included in `Brownian_sheet.pdf` and we also give the function $\tau$ (See Lemma 2.1 in *Attributes: Selective Learning and Influence*). With Lemma 2.1, we can calculate the conditional expectation and conditional variance for any observations as in the 2nd part of `Brownian_sheet.pdf`. However, since it is difficult to understand the pattern of optimal paths intuitively, we wrote code to numerically calculate the optimal path given a list of random or pre-determined realizations.

* `Numerical/sigma_gaussian_2d.m` $\sigma$ function as equation(2) in `Brownian_sheet_optimization.pdf`.
  * Input: sigma_gaussian_2d(x, y)
    * x: first point, such as x={0,1}
    * y: second point, such as y={1,2}
  * Output: their variance

* `Numerical/mu_gaussian_2d.m` $\mu$ function as equation(1) in `Brownian_sheet_optimization.pdf`.
  * Input: mu_gaussian_2d(a, mu0, mu1, mu2, type)
    * a: a point in the 2D space, such as {1,2}
    * mu0, mu1, mu2: parameters for the mean value function
    * type: the type of the mean function, either "nonlinear" or "linear"
  * Output: their mean value

* `Numerical/point_cond_expectation.m` This code is used to calculate the conditional expectation at a point $\hat{a}$ given previous observations. Refer to equation (13)-(14) in `Brownian_sheet.pdf`.
  * Input: point_cond_expectation(k_num, a_vec, f_vec, a_hat_vec, mu_type, mu0, mu1, mu2)
    * k_num: number of observation
    * a_vec: points in the 2D space, such as {{1, 2}, {2, 3}}
    * f_vec: realizations of points, such as {.1, -.5}
    * a_hat_vec: point to calculate the expectation
    * mu_type = "linear" or "nonlinear"
  * Output: condtional expectation at point a_hat_vec

* `Numerical/point_cond_variance.m` This code is used to calculate the conditional variance at a point $\hat{a}$ given previous observations. Refer to equation (18) in `Brownian_sheet.pdf`.
  * Input: point_cond_variance(k_num, a_vec, a_hat_vec)
    * k_num: number of observation
    * a_vec: points in the 2D space, such as {{1, 2}, {2, 3}}
    * a_hat_vec: point to calculate the expectation
  * Output: condtional variance at point a_hat_vec

* `Numerical/point_cond_variance.m` This code is used to calculate the conditional variance at a point $\hat{a}$ given previous observations. Refer to equation (18) in `Brownian_sheet.pdf`.
  * Input: point_cond_variance(k_num, a_vec, a_hat_vec)
    * k_num: number of observation
    * a_vec: points in the 2D space, such as {{1, 2}, {2, 3}}
    * a_hat_vec: point to calculate the expectation
  * Output: condtional variance at point a_hat_vec

* `Numerical/find_first_point.m` A function using `Global Optimization Toolbox` of MATLAB to calculate the first optimal point. Refer to equation (7) in `Brownian_sheet_optimization.pdf`.
  * Input: find_first_point(mu0, mu1, mu2, type)
    * mu0, mu1, mu2: parameters for the mean value function
    * type: the type of the mean function, either "nonlinear" or "linear"
  * Output: [point, realization]
    * point: the optimal point, such as {1,2}
    * realization: a random realization which draws from a distribution descirbed in equation (8)-(9) in `Brownian_sheet_optimization.pdf`

* `Numerical/find_next_point.m` A function using `Global Optimization Toolbox` of MATLAB to calculate the next optimal point. Refer to equation (10)-(12) in `Brownian_sheet_optimization.pdf`.
  * Input: find_next_point(mu0, mu1, mu2, type, points, realizations)
    * mu0, mu1, mu2: parameters for the mean value function
    * type: the type of the mean function, either "nonlinear" or "linear"
    * point: a list of previous optimal points, such as {{1,2},{2,3}}
    * realization: a list of previous observation, such as {.1,-.5}
  * Output: [point, realization]
    * point: the optimal point, such as {1,2}
    * realization: a random realization which draws from a distribution descirbed in equation (13)-(14), (18) in `Brownian_sheet.pdf`

* `Numerical/CondExpectation.m` This file is used to show how to use `point_cond_expectation` function to calculate all conditional expectation with within a specified region. If you are interested in the distribution of the conditional expecation, you can use this code to generate a plot.

* `Numerical/CondVariance.m` This file is used to show how to use `point_cond_variance` function to calculate all conditional variance with within a specified region. If you are interested in the distribution of the conditional variance, you can use this code to generate a plot.

* `Numerical/OptPoints.m` This code uses two functions `find_first_point` and `find_next_point.m ` to find the optimal path.

* `Numerical/test_functions.m` This is used to debug functions.

* `BrownianSheet.nb`
The purpose of this notebook is to calculate arithmetically conditionl (linear and nonlinear) expectation and variance. You can change the number of points which already exist in the space and also you can modify the mean and covariance functions before evaluate the notebook. Refer to `Brownian_sheet.pdf` for formulas.

* `BrownianSheet2.nb` (sorry for the bad name system) The purpose of this file is to have an intuition about the maximization object function about mean and variance and solve an example of it. Refer to `Brownian_sheet_optimization.pdf` for formulas.

* `BrownianSheet3.nb`
This notebook is used to calculate the optimal points given previous observations (it starts with no observation). Using functions in `Browniansheet.wl`, it can find the optimal path automatically given realizations of each rounds are randomly assigned by normal distribution in `Browniansheet.wl`. The results will be a list of points it goes through and a list of realizations for each points.

* `BrownianSheet4.nb`
This notebook is similar to `BrownianSheet3.nb`, but it is different in that we assign realizations before we find any optimal points. This is used to analyze the numerical difference between MATLAB and Mathematica.

* `BrownianSheet5.nb`
The purpose of this notebook is the same as the previous one. However, in this notebook, I use the numerical realizations we have from the MATLAB code.

* `BrownianSheet.wl`
This is a package used to calculate the optimal point given points discovered in the space. There are following functions that you can use: (Refer to `Brownian_sheet_optimization.pdf` if you want to know what those parameters stand for)
    * `FindFirstPoint` Find the first optimal point with unconditional expectation and variance function. 
        * Input: mu0_, mu1_, mu2_
        * Output: the optimal point, e.g. {0,1}

    * `RealizationFirstPoint` Draw from Normal Distribution with unconditional expectation and variance of the point.

    * `FindNextPoint` Find the next optimal point with conditional expectation and variance function. 
        * Input: previous points, previous realizations, mu0_, mu1_, mu2_
        * Output: the optimal point, e.g. {0,1}
    * `RealizationNextPoint` Draw from Normal Distribution with conditional expectation and variance of the point.
    * `PointEvaluation` evaluate the function -E^2-Var at a given point.
> * `FindFirstPoint` and `RealizationFirstPoint` works the same way as `Numerical/find_first_point.m`, and you can check the description of that file above for more details.
>  * `FindNextPoint` and `RealizationNextPoint` works the same way as `Numerical/find_next_point.m`, and you can check the description of that file above for more details.

* `Brownian_sheet.pdf` Steps and formulas for calculating conditional expectations and conditional variance.


* `Brownian_sheet_optimization.pdf` Steps and formulas for finding the optimal point given previous observations. Note: this file is different from `Brownian_sheet.pdf` in that we introduce additional parameter $\mu_0$ and linear part in $\sigma$.

* `NumericalErrorAnalysis.xlsx` The purpose of this file is to demonstrate that the Mathematica code is more accurate than the MATLAB code. We let two scripts start with same parameters. The realizations in column A is the realization of an optimal path we find with Mathematica with optimal points being points in column B and C. Column D and E are optimal points found by the MATLAB code. Column H and I are optimal points found by the MATLAB code if the history is given by Mathematica code. For example, I manually inputs those points and realizations for the first 2 rounds, and the output is the 3rd round result for column H and I; then with input being first 3 rounds of results in Mathematica, we have the 4th round result for column h and I. It shows that though the MATLAB code is pretty accurate for each round, numerical errors could accumulate quickly.