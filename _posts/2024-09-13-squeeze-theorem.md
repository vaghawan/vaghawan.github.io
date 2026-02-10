---
# cover: 'assets/images/cover6.jpg'
navigation: True
title: Squeeze Theorem and the calculation of Limit of Difficult Functions
date: 2024-09-12 10:18:00
tags:
  - mathematics
  - calculus
subclass: 'post tag-mathematics'
logo: 'assets/images/ghost.png'
author: vaghawan
categories: mathematics
usemathjax: true
author_profile: false
header:
  teaser: "unsplash-gallery-image-2-th.jpg"
---

Squeeze Theorem
---

As the name suggests, the Squeeze Theorem is actually quite an useful theorem to find the limit of a function that is squeezed between two other functions, given they meet certain properties.

Let's take an analogy of three runners in a running track. Runner 1 (\\(R_1\\)), starts at the lowest track, Runner 2 (\\(R_2\\)), starts at the middle track, and Runner 3 (\\(R_3\\)), starts at the highest track.


<img src='/images/running-track-squeeze-theorem-example.png' alt="Running track analogy for squeeze theorem">

Now, as they run, when they're about to reach the peak of the running track, \\(L\\), both \\(R_1\\) and \\(R_3\\) are at the same position, \\(L\\), then by the squeeze theorem, Runner 2 (\\(R_2\\)) at the distance \\(c\\), which was running in-between \\(R_1\\) and \\(R_3\\) in some open interval \\((a, b)\\) such that \\(c\in (a, b)\\) must also be approaching the same position, \\(L\\) as the distance approaches \\(c\\).


Now, that was an hypothetical analogy, Now, Let's imagine a more mathematical scenario:

<img src='/images/squeezed-functions.png' alt="Graph of squeezed functions">

The above figure shows three functions satisfying the following condition:

$$
f(n) \leq g(n) \leq h(n)
$$


The conditions that we must meet for this theorem to be true are:
- The limit of both \\(f(x)\\) and \\(h(x)\\) must exist and must approach the same value.
- This must hold for \\(x\\) in some open interval around \\(c\\), but this is not strictly necessary at \\(c\\) itself.

$$
f(x) \leq g(x) \leq h(x)
$$

This theorem works for both one-sided and two-sided limits as long as the above conditions are met.

---


If these conditions are met, then the Squeeze Theorem claims that as \\(g(x)\\) approaches \\(c\\),

$$
\lim_{x \to c} f(x) = L
$$

$$
\lim_{x \to c} h(x) = L
$$

Then,

$$
\lim_{x \to c} g(x) = L
$$

So, this means that if \\(g(x)\\) is sandwiched between the two functions \\(h(x)\\) and \\(f(x)\\), as \\(x\\) gets closer to \\(c\\), if both \\(h(x)\\) and \\(f(x)\\) approach the same value \\(L\\), then \\(g(x)\\) must also approach \\(L\\).

---

Squeeze theorem is simple but very powerful tool when it comes to variety of situations. For example, it comes really handly when it comes to finding the limit of fundamental trigonometric functions. It is also equally useful when it comes to figuring out the limit of indeterminate forms such as \\(\frac{0}{0}\\) and \\(\frac{\infty}{\infty}\\).



## Calculating the Limit of \\(\lim_{\theta \to 0} \frac{\sin(\theta)}{\theta}\\)

When we talk about the limit of trigonometric functions, we cannot avoid the function \\(\lim_{\theta \to 0} \frac{\sin(\theta)}{\theta} = 1\\). 
If we were to put \\(0\\) in place of \\(\theta\\), then we would immediately get undefined limit, a division by \\(0\\). But if we were to plot the graph of \\(\frac{\sin(\theta)}{\theta}\\) vs \\(\theta\\), we see that as \\(\theta\\) approaches \\(0\\), the value of the function approaches \\(1\\).

<img src='/images/sinx-by-x-desmos.png' alt="Graph of sinx by x">


Hence, we got to thik a little deeper. 
This is one of the fundamental limits in trigonometry which is useful to calculate many other limits, which are otherwise hard to evaluate.

We can use the Squeeze Theorem to calculate the limit of \\(\lim_{\theta \to 0} \frac{\sin(\theta)}{\theta}\\) by leveraging the properties of unit circle.

<img src='/images/limit-sinx-approaches-zero1.png' alt="Unit circle diagram for squeeze theorem">

Let's take the above unit circle sketch, the black traingle, lets call it \\(ABC\\), a right angled triangle. We know that the radious of the circle is \\(1\\), and the angle \\(\theta\\) is given in radians. Now, the height of the traingle, \\(AB\\) is the length of the line where hypotenous intersects the unit circle. And by the unit circle definition, the length of the line is going to be \\(\sin(\theta)\\).

Now, let's consider the blue perpendicular line \\(DE\\), which is the opposite side of the right angled traingle \\(DEC\\). If we were to calculate the tangent of the angle \\(\theta\\), we would get the length of the line \\(DE\\) as: 

$$
\tan(\theta) = \frac{\text{opposite}}{\text{adjacent}} = \frac{DE}{EC}
$$

We know that the adjacent side of the traingle \\(EC\\) is the line from the center of the circle to the point where the tangent line intersects the x-axis, which is \\(1\\). 

Hence, we can say that:

$$
\tan(\theta) = \frac{DE}{1} = DE
$$

In the first quadrant, the length of the line \\(DE\\) is positive, but in the equivalanet fourth quadrant, the length of the line \\(DE\\) will be negative. Hence we can take the aboslute value of the length of the line to make sure that it is always positive. So we take \\(\|DE\|\\) to be the length of the line \\(DE\\).

Now, let's draw anothe traingle, \\(ACE\\). 

<img src='/images/limit-sinx-all-traingles.png' alt="Unit circle diagram for squeeze theorem">

Now, let's calculate the area of this traningle, 

$$
\text{Area}_{\text{ACE}} = \frac{1}{2} . base . height = \frac{1}{2} . CE . AE = \frac{1}{2} \sin(\theta)
$$

Now, we know that, even this larger traingle doesn't completly cover the wedge (red colored fraction \\(ACE\\)) of the circle made by the hypotenuse \\(AC\\). From the unit circle definition, we know that the whole circle is \\(2(\pi)\\) radian, then this wedge covers \\(\frac{\theta}{2\pi}\\) of the whole circle.
Now from the area of the circle, we know that the area of the whole circle is \\(\pi\\), hence the area of the wedge, which is actually a smaller circle with angle \\(\theta\\) is \\(\frac{\theta}{2\pi} . \pi = \frac{\theta}{2}\\).


Now, let's calculate the area of the larger traingle \\(DCE\\).

$$
\text{Area}_{\text{DCE}} = \frac{1}{2} . base . height = \frac{1}{2} . CE . DE = \frac{1}{2} \tan(\theta)
$$

Now, the area of the samller traingle \\(ACE\\) is always less than the area of the wedge also colored red \\(ACE\\), which is always less than the area of the larger traingle \\(DCE\\). Hence, we can say that:

$$
f(\theta) \leq g(\theta) \leq h(\theta); \\
\text{ for } \frac{\pi}{2} \leq \theta \leq \frac{\pi}{2}
$$

In the above statement, \\(f(\theta)\\) is the area of the smaller traingle \\(ACE\\), \\(g(\theta)\\) is the area of the wedge \\(ACE\\), and \\(h(\theta)\\) is the area of the larger traingle \\(DCE\\).

Substituting the values of the areas, we get:

$$
\frac{1}{2} \sin(\theta) \leq \frac{1}{2} \theta \leq \frac{1}{2} \tan(\theta)
$$

Dividing the whole inequality by \\(\frac{1}{2}\\), we get:

$$
\sin(\theta) \leq \theta \leq \tan(\theta)
$$

$$
\sin(\theta) \leq \theta \leq \frac{\sin(\theta)}{\cos(\theta)}
$$

Now, let's divide the whole inequality by \\(\sin(\theta)\\), which is always positive for \\(\theta \in (-\frac{\pi}{2}, \frac{\pi}{2})\\).

$$
1 \leq \frac{\theta}{\sin(\theta)} \leq \frac{1}{\cos(\theta)}
$$

Taking the reciprocal of the inequality, we get:

$$
1 \geq \frac{\sin(\theta)}{\theta} \geq \cos(\theta)
$$

Now, as \\(\theta\\) approaches \\(0\\), \\(\cos(\theta)\\) approaches \\(1\\). Hence, by the Squeeze Theorem, we can say that:

$$
\lim_{\theta \to 0} 1 \geq \lim_{\theta \to 0} \frac{\sin(\theta)}{\theta} \geq \lim_{\theta \to 0} \cos(\theta)
$$

$$
1 \geq \lim_{\theta \to 0} \frac{\sin(\theta)}{\theta} \geq 1
$$

$$
\lim_{\theta \to 0} \frac{\sin(\theta)}{\theta} = 1
$$

This is the beauty of the Squeeze Theorem, which made it possibly to intituvely evaluate the limits of \\(\lim_{\theta \to 0} \frac{\sin(\theta)}{\theta} = 1\\).

-----

To Do : Proof of the Squeeze Theorem



## References

1. Khan Academy. (n.d.). [Squeeze (sandwich) theorem](https://www.khanacademy.org/math/differential-calculus/dc-limits/dc-squeeze-theorem/v/squeeze-sandwich-theorem). 

2. Khan Academy. (n.d.). [Sinx/x as x approaches 0](https://www.khanacademy.org/math/differential-calculus/dc-limits/dc-squeeze-theorem/v/sinx-over-x-as-x-approaches-0). 




