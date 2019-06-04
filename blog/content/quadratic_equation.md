Title: Simple Math Post - Quadratic Equation
Date: 2019-06-03 20:17
Category: Technical
Tags: algebra, testing
Authors: Aditya Gudibanda

This is just a "filler" post to keep the content coming.


Let's prove the quadratic formula. We'd like to solve for $x$ in the equation

$$ax^2 + bx + c = 0$$

Let's start with some transformations.

$$x^2 + \frac{b}{a}x + \frac{c}{a} = 0$$

Next, we complete the square:

$$\left(x + \frac{b}{2a}\right)^2 - \frac{b^2}{4a^2} + \frac{c}{a} = 0$$
$$\Rightarrow \left(x + \frac{b}{2a}\right)^2 - \frac{b^2 - 4ac}{4a^2} = 0$$
$$\Rightarrow \left(x + \frac{b}{2a}\right)^2 = \frac{b^2 - 4ac}{4a^2}$$
$$\Rightarrow x + \frac{b}{2a} = \pm \sqrt{\frac{b^2 - 4ac}{4a^2}}$$
$$\Rightarrow x =  \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

as desired.


