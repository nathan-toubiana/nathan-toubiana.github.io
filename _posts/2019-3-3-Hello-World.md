---
layout: post
title: Scitime
---

[Scitime](https://github.com/nathan-toubiana/scitime) is a package that provides training time estimation for scikit-learn algorithms. The main function in this package is called “time”. Given a matrix vector X, the estimated vector Y along with the Scikit Learn model of your choice, time will output both the estimated time and its confidence interval.
Let’s say you wanted to train a kmeans clustering for example, given an input matrix X. Here’s how you would compute the runtime estimate:

```python
from sklearn.clusters import KMeans
from scitime import Estimator 
kmeans = KMeans()
estimator = Estimator(verbose=3) 
# Run the estimation
estimation, lower_bound, upper_bound = estimator.time(kmeans, X)
```

We are able to predict the runtime to fit by using our own estimator, we call it meta algorithm (meta_algo), whose weights are stored in a dedicated pickle file in the package metadata.

The meta algos estimate the time to fit using a set of ‘meta’ features, including the parameters of the algo itself (in this case kmeans) and also external parameters such as cpu, memory or number of rows/columns.

We built these meta algos by generating the data ourselves using a combination of computers and VM hardwares to simulate what the training time would be on the different systems, circling through different values of the parameters of the algo and dataset sizes .
