# Ml-Reco-Books 

Here are peace of codes, that recommend us some books according to their categories.

Domain is composed of
- Set all books
- Set of favorite books
- Each book has qualified and valued categories (ex: <classic: 10.0>, <history: 2.0>)

Goals
- recommend a book based on favorite ones
- draw 3d positions after feature elimination base on low variance
- demonstrate PCA derivation by lagrangian and eigen values and vectors

## Technical components
- C++ written library
- Python client app to call .so library and plot (matplotlib & numpy)

## Simplified diagram

![variance](./images/ml-reco-books/diagram.png)

## Recommendation by distances

A simple approach is first to compute the centroid of our cluster aka our favorite books. Then we compute the distances between all others books. Books are defined by rated categories which are our features.
We pickup the one with the smallest distances.   
There are many ways to compute distances here are some:
- Euclidian
- Cosine
- Manathan
- Mahanlobis

![variance](PycharmProjects/ml-reco-books/distances.png)

## Feature elimination

When we deal with high dimensional data, we want to reduce that dimensionality without
loosing too much information and keeping the important one.  

The first step is by knowing well the problem we want to solve.  
Asking the question "is that feature meaningful to characterize by data ?"  

To select or remove feature we can observe correlation between features, chi squared test... there plenty you can find online.

In our first case by choice, in order to plot it we will keep only the ones with high variances. We could have done PCA but I wanted only to derive it.

The second case we will see with PCA how we can maximize the information during a dimension reduction.


 
![variance](PycharmProjects/ml-reco-books/scatter.png)


## Mathematical derivation of Principal Component Analysis, why we end up by searching eigen vectors

PCA is helpful to reduce dimensions and keeping information. Because of its geometrical property some people use it to 
visualise data. We will se why and how.




If we think features as vectors.
Geometrically is the same as saying I want to project (x1,x2) onto (x4, x5). So the aim of PCA is trying find those vector without loosing information (=keeping high variance)
  
Doing that will end up by computing eigen vectors, by first finding their eigen values, here is a method by using the Variance matrix.


First we start by defining the variance of the projected data :
   
![variance](PycharmProjects/ml-reco-books/variance.png)

We put S as the following

![variance](PycharmProjects/ml-reco-books/s_variance.png)

From there we want to maximize the variance of the project aka try to projected feature but not loosing information from removed features, far from the mean.  

To maximize a multivariate equation with constraint (here ||v|| = 1, unitary vector), we can use a Lagrangian
  
![variance](PycharmProjects/ml-reco-books/lagrangian.png)
 
 After arranging the equation, to maximize it we compute the gradient of it
 
 ![variance](PycharmProjects/ml-reco-books/gradient.png)
 
 So we end up with an equation with tha form 
 
 ![eigen equation](PycharmProjects/ml-reco-books/eigen_equation.png)
 
 Resolving this equation is equivalent to find eigen vectors and eigen values. Just pick the highest ones.
 
 With few lines of code, Python package sklearn is doing all that for us :).
 
 Samy Badjoudj
 
 