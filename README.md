
# Computational Complexity: From OLS to Gradient Descent

## Introduction

In this lesson, we’ll introduce you to the area of computational complexity. We will relate this idea to the OLS regression and see how this may not be the MOST efficient algorithm to calculate the regression paramaters when performing regression with large datasets. We shall set a stage for an optimization algorithm called "Gradient Descent" which will be covered in detail in the following section of this module. 

## Objectives

You will be able to:

* Understand and explain why Ordinary Least Squares using Matrix algebra could become problematic for large/complex data
* Understand basics of computational complexity in terms on Big-O notation
* Explain how a machine learning optimization technique like gradient descent can solve the complexity issues 

## Complexities in OLS

Recall the OLS formula for calculating the beta vector:
####    β = (X′ .  X) <sup>−1</sup> .  X′ .  Y

This formula looks very simple, elegant and intuitive. It works perfectly fine for the case of simple linear regression due to limited number of computed dimensions, but with datasets which qualify as very large or BIG DATA sets, it becomes computationally very expensive as it can potentially involve a huge number complex mathematical operations. 

For this formula, we need to find (X′ .  X)  , and invert it as well, which makes it very expensive. Imagine is matrix X<sub>(N x M+1)</sub> has M+1 columns where M is the number of predictors and N is the number of rows of observations. In a machine learning practice, you will often find datasets with M >1000 and N > 1,000,000. The X′X matrix itself takes a  while to calculate, then you have to invert M×M matrix which adds more to the complexity -  making it hugely expensive. It may also be the case the input matrix grows so large that it can not fit into your computer's memory. 

### The Big-O Notation

In computer science, Big O notation is used to describe how ‘fast’ an algorithm grows, by comparing the number of operations within the algorithm. Big O notation helps you see the worst-case scenario for an algorithm. Typically, we are most concerned with the Big O time because we are interested in how slowly a given algorithm will possibly  run at worst.

#### Example

What’s the most straightforward way of finding this person? Well, you could go through every single name in the phone book until you find your target. This is known as a simple search. If the phone book is not very long, with say, only 10 names, this is a fairly fast process. But what if there are 10,000 names in the phone book?

At best, your target’s name is at the front of the list and you only need to need to check the first item. At worst, your target’s name is at the very end of the phone book and you will need to have searched all 1000 names. As the ‘dataset’ (or the phone book) increases in size, the maximum time it takes to run a simple search also linearly increases.

In this case, our algorithm is a simple search. Big O notation allows us to describe what our worst case is. Our worst case is that we will have to search through all elements (n) in the phone book. We can describe the run-time as:

> **O(n) where n: number of operations**

Because the maximum number of operations is equal to the maximum number of elements in our phone book, we say the Big O of a simple search is O(n). **A simple search will never be slower than O(n) time.**

Different algorithms have different run-times. That is, algorithms grow at different rates. The most common Big O run-times, from fastest to slowest, are:

* O(log n): aka log time
* O(n): aka linear time
* O(n log n)
* O(n²)
* O(n<sup>3</sup>)
* O(n!)

This can be shown in following figure:
![](bigo.jpeg)

### OLS and Big-o Notation

Inverting a matrix costs **O(n<sup>3</sup>)** for computation where n is the number of rows in X matrix i.e. the observations. Here is an explanation on how to calculate Big-O for OLS.
```
The linear regression is computed as (X'X)^-1 X'Y.

If X is an (n x k) matrix:

(X' X) takes O(n*k^2) time and produces a (k x k) matrix

The matrix inversion of a (k x k) matrix takes O(k^3) time

(X' Y) takes O(n*k^2) time and produces a (k x k) matrix

The final matrix multiplication of two (k x k) matrices takes O(k^3) time

```
#### So the Big-O running time for OLS is O(k<sup>2*(n + k)</sup>) - NOW THATS EXPENSIVE.

#### If the X is ill conditioned  i.e. it isnt a square matrix etc., then it will create computational errors in estimation. 

#### Another problem is overfitting and underfitting in estimation of regression coefficients that can't be helped too much with Ordinary Least Squares.

So, this leads us to the Gradient Descent kind of optimization algorithm which can save us from this type of problem. The main reason why gradient descent is used for linear regression is the computational complexity: it's computationally cheaper (faster) to find the solution using the gradient descent in most cases.

## Gradient Descent 
![](grad.png)

> Gradient Descent is an iterative approach to minimize the model loss (error), used while training a machine learning model like linear regression. It is an optimization algorithm based on a convex function as shown in the figure above, that tweaks it’s parameters iteratively to minimize a given function to its local minimum.

In regression, it is simply used to find the values of model parameters (coefficients) that minimize a cost function (like RMSE) as far as possible.

In order to fully understand how this works, you need to know what a gradient is and how is it calculated. And for this, you would need some Calculus. Right this may sound a bit intimidating at this stage , but dont worry. Following section covers basic of calculus with gradients and derivatives. 

and by the way ..

#### WELCOME TO MACHINE LEARNING 
![](https://i0.wp.com/dataandstats.com/wp-content/uploads/2017/12/machine-learning-joke.jpg?resize=638%2C359&ssl=1)

## Further Reading

[Wiki: Computational Complexity of mathematical Operations](https://en.wikipedia.org/wiki/Computational_complexity_of_mathematical_operations)

[Simplified Big-O notation](https://medium.com/karuna-sehgal/a-simplified-explanation-of-the-big-o-notation-82523585e835)

[Gradient Descent in a nutshell](https://towardsdatascience.com/gradient-descent-in-a-nutshell-eaf8c18212f0)


## Summary 

In this lesson, we looked at the shortcomings and limitations of OLS and matrix inverses. We looked at the Big-O notation to explain how calculating inverses and transposes for large matrix might make our analysis unstable and computationally very expensive.  This lesson sets a stage for your next section " Calculus and Gradient Descent".You will have a much better understanding of the gradient descent diagram shown above and how it all works by the end of next section. 
