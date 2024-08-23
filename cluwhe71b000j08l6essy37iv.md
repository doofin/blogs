---
title: "Complex systems, Chaos and ecosystem part 1: the defiance to  reductionism"
seoTitle: "Chaos and Ecosystems: Beyond Reductionism"
seoDescription: "An overview of reductionism's limitations and the basics of dynamical systems and chaos theory in understanding complex systems"
datePublished: Fri Apr 12 2024 09:44:09 GMT+0000 (Coordinated Universal Time)
cuid: cluwhe71b000j08l6essy37iv
slug: complex-systems-chaos-and-ecosystem-the-defiance-to-reductionism
tags: complexity, mathematics

---

Reductionism, a philosophy that seeks to handle complexity by breaking into parts, serves as the corner stone for industrial revolution and contemporary science. This top-down approach is also quite compatible with the social hierarchy that rich people have more power and control over the society, as the conerstone of modern neoliberal capitalism.  
  
However, The whole is often greater than the sum of its parts, and the attempt to understand complex systems through reductionism neglects the interactions, emergent behaviors, and non-linear dynamics within the system.  
  
In neuroscience and artificial intelligence, attempting to understand consciousness through the examination of individual neurons can't answer how consciousness emerge from those simple parts, as well as trying to create intelligence by connect neurons in a predefined way, whatsoever it's convolutional, hierarchical or recurrent. Similarly, In ecology, reducing an ecosystem to its individual species is unable to explain the stability,resilience and at the same time, the fragility of ecosystem.  
  
Aside from those complicated systems, simple deterministic system may show unpredictable behaviors. In this article, I will introduce the concept of dynamical systems and show some of those systems described with simple mathematical formula.  
  
In this part 1 note, basic concepts of dynamical systems like phase space, trajectory, bifurcation, Feigenbaum constant will be introduced, and we mostly focus on examples.  
Advanced concepts like chaos, renormalization, self-organization will be discussed in the next part, as well as the mathematical tools.

## Define Chaos

For a particular **mathematical formula or computation process**(like calculate the trajectory of three body system, predict weather ,etc), a slightly different **initial condition, or input, would result in very different result**.

What does this sensitivity implies? For an computation process to be useful, we usually expect to get similar result for similar input, otherwise the output is not meaningful since a small rounding error will invalidate the result.

## sensitivity to initial condition

To display the essence of chaotic behavior, we start from simple deterministic mathematics formulas.

[Example](https://en.wikipedia.org/wiki/Three-body_problem): a slightly different [initial condition would result in](https://en.wikipedia.org/wiki/Initial_condition) a vastly different [trajectory](https://en.wikipedia.org/wiki/Trajectory)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712259710907/ad57dd53-75f4-4074-9178-ffb93e22e0a9.png align="center")

[Example](https://en.wikipedia.org/wiki/Three-body_problem): Three 2 node system with slightly different initial condition:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e3/Demonstrating_Chaos_with_a_Double_Pendulum.gif/220px-Demonstrating_Chaos_with_a_Double_Pendulum.gif align="left")

![File:Double-compound-pendulum.gif](https://upload.wikimedia.org/wikipedia/commons/4/45/Double-compound-pendulum.gif align="left")

[Example](https://en.wikipedia.org/wiki/Three-body_problem): logistic map

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712259209275/bac24936-d763-4373-8903-26d334915a53.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712259303803/4c6513eb-ac41-4c8a-ab06-fa56cfdce427.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712259351580/158e910a-6a61-4e69-8d42-7c32b31dd517.png align="center")

Example: Three-body problem

![](https://upload.wikimedia.org/wikipedia/commons/1/1c/Three-body_Problem_Animation_with_COM.gif align="left")

Example: Biosphere II was a expensive failure to create a self-sustaining replica of Earth ecosystems.

Example

while we are sure about our location in the short run, we can not say precisely where we are at a specific date in the long run, for example in a year.

## Describe and analyze Chaos: dynamical systems theory

Although we can't calculate chaotic system in the usual way, there are some new tools that will shed some light.

### bifurcation diagram

for the logistic map example we just discussed, this diagram plots the stabilized x value versus the parameter R:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712259390336/03a37aba-c6b8-489b-9643-68dad0cd8f8a.png align="center")

As the parameter R increase at 3.0, X have more possible values.

### phase space

In dynamical systems theory and control theory, a **phase space** or state space is a space to display all possible "states"(positions), in contrast to the **trajectory**(position at specific time t) of the system.

Example: [https://verzep.github.io/Learning-Lorenz/](https://verzep.github.io/Learning-Lorenz/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712914723307/80e5097c-7187-416c-93ad-16221073e5f3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712914698411/d495b82d-95c1-4d9b-9c69-bf18b9e58f2a.png align="center")

In space (x,y,z) - time

![Chaos theory and global warming: can climate be predicted?](https://skepticalscience.com/images/chaos1.gif align="left")

In phase space (x,y,z):

![](https://miro.medium.com/v2/resize:fit:1313/1*4zLik4-PUVjdBDAp3BpWSQ.png align="left")

### Feigenbaum constant:

The constant represents the ratio of the difference in parameter values at which successive bifurcations occur as a system undergoes a period-doubling route to chaos. It has an approximate value of 4.6692.

TBD

## AI and the failed prediction of Chaos

TBD  
Lorenz System [https://verzep.github.io/Learning-Lorenz/](https://verzep.github.io/Learning-Lorenz/)

# Reference:

[https://en.wikipedia.org/wiki/Three-body\_problem](https://en.wikipedia.org/wiki/Three-body_problem)

Complexity: A Guided Tour , by Melanie Mitchell

[https://en.wikipedia.org/wiki/Chaos\_theory](https://en.wikipedia.org/wiki/Chaos_theory)

lorenz equation: [https://www.math.fsu.edu/~bertram/lectures/Chaos.pdf](https://www.math.fsu.edu/~bertram/lectures/Chaos.pdf)

[https://verzep.github.io/Learning-Lorenz/](https://verzep.github.io/Learning-Lorenz/)

[https://gereshes.com/2018/11/19/chaos-and-the-double-pendulum/](https://gereshes.com/2018/11/19/chaos-and-the-double-pendulum/)

### QA:

I presented this in a meeting and got some good questions:

Are chaotic systems calculable?

yes, if you have extremely accuracy of the initial condition. There're two way to address this: 1. we continue to quest for higher precision. 2. we accept this difficulty and give up for precise prediction/computation

In addition, someone mentioned Kolmogorov–Arnold–Moser about the persistence of quasiperiodic motions under small perturbations, which can be seen as a special case when computation is desirable.