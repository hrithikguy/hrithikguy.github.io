Title: First Math Post - Distance from a point to a line in 2D
Date: 2019-05-24 18:44
Category: Technical
Tags: geometry, testing
Authors: Aditya Gudibanda


How do you calculate the distance from a point to a line? 

First of all, why would you want to?  There could be many reasons, but I'm interested in it right now because it comes up in machine learning classification problems. For example, perceptrons and support vector machines (SVMs) entail the concept of a "margin" in classification. The intuition for margin is the idea that, given a set of points divided into two classes, we would like to find the line dividing the classes which maximizes the distance to the closest point. Intuitively, this will avoid overfitting on the test data, because the line does not get unnecessarily close to any point when it doesn't have to - this preserves "uncertainty". 

So in order to find a separating line which maximizes the margin, we need to be able to mathematically express the margin so that we can incorporate it into a loss function to minimize.

I will be doing this for two dimensions.


Suppose we have a line $l$ given by the equation $y = mx + b$, and we have a point $P = (c,d)$. We would like to compute the distance from $P$ to $l$.

We will do this by computing the distance between $P$ and an arbitrary point on $l$, $Q(r)= (r, mr + b)$, parametrized by the variable $r$. Then we will find the $r$ which minimizes this distance. This is equivalent to minimizing the square of the distance, so we will minimize that instead.

The distance squared is 
$$f(r) = || P - Q(r) || ^2 = (c - r)^2 + (mr + b - d)^2$$

 To find the $r$ which minimizes this, we set the derivative equal to $0$.

$$\frac{d f(r)}{dr} = 2(c-r)(-1) + 2 (mr + b - d) (m)$$
$$ = -2c + 2r + 2m^2r + 2mb - 2md = r(2 + 2m^2) + (2mb - 2md - 2c) = 0$$ 

Solving for $r$, we get 
$$r = \frac{2c + 2md - 2mb}{2 + 2m^2} = \frac{c + md - mb}{1 + m^2}$$

This is the $x$-coordinate of the point on $l$ closest to $P$. The $y$ coordinate is given by 
$$mr + b = \frac{mc + m^2d-m^2b + b + bm^2}{1 + m^2}$$
$$ = \frac{mc + m^2d + b}{1 + m^2}$$

Let $Q' $ be the closest point to $P$ on $l$, given by 
$$Q' = Q\left(\frac{c + md - mb}{1 + m^2}\right)$$
$$= \left(\frac{c + md - mb}{1 + m^2}, \frac{mc + m^2d + b}{1 + m^2}\right)$$

We need the distance from $Q' $ to $P$.


This is given by 
$$\sqrt{ \left(  c - \frac{c + md - mb}{1 + m^2}  \right)^2 + \left(  d - \frac{mc + m^2d + b}{1 + m^2}  \right)^2  }$$

$$=\sqrt{ \left(  \frac{c + cm^2 - c - md + mb}{1 + m^2}  \right)^2 + \left(  \frac{d + dm^2 - mc - m^2d - b}{1 + m^2}  \right)^2  }$$
$$= \sqrt{ \left(  \frac{cm^2- md + mb}{1 + m^2}  \right)^2 + \left(  \frac{d - mc - b}{1 + m^2}  \right)^2  }$$
$$= \sqrt{ \left(  \frac{m (cm - d + b)}{1 + m^2}  \right)^2 + \left(  \frac{cm - d + b}{1 + m^2}  \right)^2  }$$
$$= \sqrt{ \frac{m^2 (cm - d + b)^2 + (cm - d + b)^2}{(1 + m^2)^2} }$$
$$= \sqrt{ \frac{(m^2 + 1)(cm - d + b)^2}{(1 + m^2)^2}}$$
$$= \sqrt{ \frac{(cm-d+b)^2}{1 + m^2}  }$$
$$= \frac{cm -d + b}{\sqrt{1 + m^2}}$$

and that is our final answer to the distance from $P = (c,d)$ to the line $l$, given by $y = mx + b$.





