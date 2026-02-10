---
# cover: 'assets/images/cover6.jpg'
navigation: True
title: Upper Bounds and So on ..
date: 2025-12-09 10:18:00
tags:
  - mathematics
  - analysis
subclass: 'post tag-mathematics'
logo: 'assets/images/ghost.png'
author: vaghawan
categories: mathematics
usemathjax: true
author_profile: false
header:
  teaser: "unsplash-gallery-image-2-th.jpg"
---

Upper Bounds and So on ..
---


You may be thinking that this is going to be a deep mathematical stuffs, but unfortunately no! This is going to remain as simple as possible

We're acutely aware and some of us may rather be thrilled with the following expression:


A **function** $f:X\rightarrow \mathbf{R}$ is bounded above on $X$ if and only if $\exists M \in \mathbf{R}$ s.t. $f(x)\le M$. (i)

For a very long time, I was stuck at this very point of analysis. As most students have the same feeling about epsilon and delta, I too just wanted to manage and get away, at least for the sake of exams.

Then after many years I found the book, ***How to Analysis*** by Lara Alcock. I can't emphasize how the book shaped my understanding of analysis, even only in first few pages.

The above definition is something that I literally copied from the book. First of all, it is also important that we know to put this definition into plain words.

---


The equation (i) we saw above means:

> "A **function** $f$ from the set $X$ to the reals is bounded above on $X$ if and only if there exists $M$ in the reals such that for all $x$ in $X$, the function $f(x)$ is less than or equal to $M$".

This definition basically defines a property of a **function** $f$, from set $X$ to reals. This is also written as $f: X \rightarrow \mathbf{R}$. $f$ takes $x$ as inputs and outputs the real numbers. One thing that we must realize at this point is that this function is defined for every real number, so the domain of this function is $X=\mathbf{R}$.

To see whether or not this function is bounded above, we need to check whether or not this definition is satisfied.

---

Let's concretize this abstract function $f$ into something simpler and familiar: $f(x)=x^{2}$.

Now for $f(x)=x^{2}$ to be bounded above on $f: \mathbf{R}\rightarrow \mathbf{R}$, $\exists M\in \mathbf{R}$ such that $\forall x\in \mathbf{R}$, $x^{2}\le M$.

Now, let's plot this function. Let's take any arbitrary point $M$. Does it satisfy the condition $f(x) \le M$?

<img src='/images/fx-image-1.jpg' alt="function of x squared">


Let's take any arbitary point $M$, does it satisfies the condition $f)x) \leq M$?

In other words, we need to check whether values in the vertical axis are less than or equal to $M$. 
Clearly, in our figure, the choosen $M$ does not satisfy this condition. 

However, we're broadly interested in knowing whether there exists such $M$ such that $f(x) \le M$ , $\forall x \in \mathbf{R}$. 
The function $f(x) = x^2$, on $X \in \mathbf{R}$, can go on and on, and we can always find another $x$, for which $f(x) > M$. So, no, there is no such $M$, no matter how large a $M$ that we choose.

So, this function is **not bounded above** particularly on this domain $X=\mathbf{R}$.

---

### Domain Restriction

But does that also mean $f(x) = x^2$ is never bounded above?

**No!** Let's say we choose a domain $X \in [0, 2]$.
We then plot the function $f(x)=x^{2}$ again. , showing $M=4$ as an upper bound.

<img src='/images/fx-image-2.jpg' alt="function of x squared">

As we can see, in this domain, clearly when we choose $M \ge 4$, the function $f(x)$ is **bounded above**.

Another thing to notice here is that any values greater than or equal to 4 will work. That means there can be as many $M$ and it doesn't necessarily have to be a single value as our definition does not complain about that explicitly or neither say a perfect bound.

---

### Example 2: $f(x) = \sin(x)$

To help us understand more, let's take a function $f(x) = \sin(x)$. It is clearly **bounded above** by $M \ge 1$. It is also bounded above by $M=2$, since $\sin(x) \le 2$ and so on.

<img src='/images/fx-sinx-image-3.png' alt="function of sin(x)">




---



Now, let's consider the function $f(x) = 3-x^2$. As you can imagine, this is clearly **bounded above by 3**.

But what about **bounded below**?

This is a little exercise question that the book poses: could you write down a definition of **bounded below** and confirm this?

So, let's write that in fact:
> A **function** $f: \mathbf{R} \rightarrow \mathbf{R}$ given by $f(x) = 3-x^{2}$ is **bounded below** in $\mathbf{R}$ if and only if $\exists m \in \mathbf{R}$ s.t. $\forall x\in \mathbf{R}$, $f(x) \ge m$.



So, as you can notice, 3 is the upper bound of this function. We can **not find any $m$** such that $f(x)\ge m$. For the function $f(x) = 3-x^{2}$, it goes on and on with the negative values in the vertical axis.

<img src='/images/fx-image-3.jpg' alt="function of 3 - x squared">

So, while this function is **bounded above** ($f(x) \le 3$), this function is **not bounded below**, as there is no $m$ to satisfy the definition.

Again, if we **restrict the domain**, then we can definitely have the function **bounded below**, but when $X = \mathbf{R}$, it is clearly not.





## References

1.  [How to Think About Analysis by Lara Aclock](https://www.amazon.com/Think-About-Analysis-Lara-Alcock/dp/0198723539)






