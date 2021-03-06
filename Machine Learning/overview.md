* Effective number of parameters of KNN
* cross-entropy
* Smooth coordinate functions
* Degree of freedoms
* Gauss-Markov Theorem
* Triangle inequality
* Gram-Schmit Procedure
* 

# Overview
1. In the book ESL (The Element of Statistical Learning), the supervised learning (e.g. regression and classification) problem is treated as a problem in function approximation. In terms of function approximation, we imagine our parameterized function as a surface in p + 1 space, and what we observe are noisy realizations from it. (Section 2.6.3)
1. A large subset of the most popular techniques in use today are variants of two simple procedures: Least Squares and KNN.

# Philosophy
* It is important to understand the ideas behind the various techniques, in order to know how and when to use them.
* One has to understand the simpler methods first, in order to grasp the more sophisticated ones.
* It is important to accurately assess the performance of a method, to know how well or how badly it is working. Simpler methods often
perform as well as fancier ones!
* 


# Linear Model
1. The linear model makes huge assumptions about structure and yields stable but possibly inaccurate preditions. It has low variance and potentially high bias.

## Extentions
1. Local regression fits linear models by locally weighted least squares, rather than fitting constants locally.
1. Linear models fit to a basis expansion of the original inputs allow arbitrarily complex models.
1. Projection pursuit and neural network models consist of sums of non-linearly transformed linear models.

# K-nearest neighbors (KNN)
1. The method of k-nearest neighbors make very mild structural assumptions about the underlying data: its predictions are often accurate but can be unstable. Any particular subregion of the decision boundary depends on a handful of input points and their particular positions, and is thus wiggly and unstable. It has high variance and low bias.
1. The error on the training data should be approximately an increasing function of k, and will always be ```0``` for ```k = 1```.
1. It appears that KNN fits have a single parameter, the number of neighbors k, compared to the ```p``` parameters in least-squares fits. However the effective number of parameters of KNN is **```N/k```** and is generally bigger than ```p```, and decreases with increasing ```k```.
1. It is also clear that we cannot use sum-of-squared errors on the training set as a criterion for picking ```k```, since we would always pick ```k = 1```!

## Extension of KNN
1. Kernel methods such as kernel smoothers, that use weights that decrease smoothly to zero with distance from the target point, rather than the effective ```0/1``` weights used by KNN. In high-dimensional spaces the distance kernels are modified to emphasize some variable more than others.
1. Nearest-neighbor methods can be thought of as kernel methods having a more data-dependent metric.

## Why KNN (and other local methods) doesn't work in high dimension and the Curse of dimensionality? 
* **Definition**: As the dimensionality of the features space increases, the number configurations can grow exponentionally, and thus the number of configurations covered by an observation decreases. (Chris Albon). 
* Any method that attempts to produce locally varying functions in small isotropic neighborhoods will run into problems in high dimensions. 
### Why KNN failed in high dimension? 
It becomes difficult to gather K observations close to a target point x0.
1. Near neighborhoods tend to be spatially large, and estimates are biased.
   1. Sparse sampling makes local neighborhoods (which is used to approximate the theoretically optimal conditional expectation by KNN averaging) in high dimension no longer local: For example, to capture 1% or 10% of the data in a unit hypercube, we must cover 63% or 80% of the range of each input variable. Such neighborhoods are no longer local. 
1. Reducing the spatial size of the neighborhood means reducing K, and the variance of the estimate increases. The fewer observations we average, the higher is the variance of our fit.
1. Most data points are closer to the boundary of the sample space than to any other data point: This makes prediction much more difficult near the edges of the training sample. One must extrapolate from neighboring sample points rather than interpolate between them.
1. In high dimensions all feasible training samples (The samples are assumed to come from the unknown true probability distribution of data, and each sample has many data points) sparsely populate the input space: The [sampling density, i.e. the number of recorded samples per unit distance along a dimension](https://math.stackexchange.com/questions/283006/what-is-a-sampling-density-why-is-the-sampling-density-proportional-to-n1-p) is proportional to N<sup>1/p</sup>, where ```p``` is the dimension of the input space and ```N``` is the sample size. To keep the same density, the sample size has to grow exponentionally, which is infeasible with high dimension.
1. The complexity of functions of many variables (i.e. the truth relationship of data) can grow exponentially with the dimension, and if we wish to be able to estimate such functions with the same accuracy as function in low dimensions, then we need the size of our training set to grow exponentially as well.

## The Need for Structured approaches
1. We can avoid the curse of dimensionality by imposing some heavy restrictions (e.g. assume data is linear) on the class of models being fitted. 
   * Of course, if the assumptions are wrong, all bets are off and the 1-nearest neighbor may dominate. 
   * There is a whole spectrum of models between the rigid linear models and the extremely flexible 1-nearest-neighbor models, each with their own assumptions and biases, which have been proposed specifically to avoid the exponential growth in complexity of functions in high dimensions by drawing heavily on these assumptions.
   * All methods that overcome the dimensionality problem have an associated -- and often implicit or adaptive -- metric for measuring neighborhoods, which basically does NOT allow the neighborhood to be simultaneously small in all directions.  

1. Structured approaches can make more efficient use of the data.
1. If we think of the supervised learning problem as function approximation, for finite number of training data, there can be infinitely many solutions: any function passing through the training points is a solution. We must therefore restrict the eligible solutions to a smaller set of functions. 
   * How to decide on the nature of the restritions (called **complexity restrictions**) is based on considerations outside of the data. 
   * This usually means some kind of regular behavior in small neighborhoods of the input space. 
   * The strength of the constraint is dictated by the neighborhood size. The larger the neighborhood size the stronger the constraint.
   * The nature of the constraint depends on the metric used.

# Classes of Restricted Estimators
## Roughness Penalty and Bayesian Methods
## Kernel methods and local regression
1. These methods can be thought of as explicitly providing esti mates of the re-gression function or conditional expectation by specifyin g the nature of the local neighborhood, and of the class of regular functions fit ted locally.

## Basis functions and dictionary methods
1. Radial basis functionsare symmetricp -dimensional kernels located at particular centroids.
1. A single-layer feed-forward neural network model with linear output weights can be thought of as an adaptive basis function method. 
1. These adaptively chosen basis function methods are also known as dictio-narymethods, where one has available a possibly infinite set or di ctionary Dof candidate basis functions from which to choose, and models are builtup by employing some kind of search mechanism.

# Model Selection and the Bias–Variance Tradeoff
1. Unfortunately training error is not a good estimate of test error, as it does not properly account for model complexity.






