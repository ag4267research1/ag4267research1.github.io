---
title: "Optimal Control Problems"
date: 2026-03-05
draft: false
author: "Anish Ghosh"
math: true
tags: ["optimization", "pde", "control"]
categories: ["mathematics", "scientific-computing"]
description: "A short introduction to optimal control problems and their computational aspects."
---

Optimal control problems arise when we want to **determine a control variable that optimizes a given objective while satisfying dynamical or physical constraints**. These problems appear naturally in engineering, physics, economics, and many areas of applied mathematics.

A classical formulation can be written as

$$
\min_{u} J(u)
$$

subject to a constraint

$$
c(x,u)=0
$$

where \(x\) typically represents the **state variable** governed by a differential equation and \(u\) represents the **control**.

In many applications the constraint takes the form of a **partial differential equation**

$$
A(u)x = f
$$

which leads to the class of **PDE-constrained optimization problems**.

## Adjoint Method

A common approach for computing gradients efficiently is the **adjoint method**.  
Instead of differentiating the constraint explicitly, an adjoint equation is introduced:

$$
A(u)^T p = \frac{\partial J}{\partial x}.
$$

This allows the gradient of the reduced objective to be computed as

$$
\nabla \hat J(u) =
\frac{\partial J}{\partial u} -
\left\langle p , \frac{\partial c}{\partial u} \right\rangle.
$$

Adjoint methods are widely used in **scientific computing, optimal control, and inverse problems**.

## Illustration

![Optimal Control Illustration](/img/blog/optimal-control.png)
<!-- 
*Example diagram of a control system.*

## Remarks

Many modern research directions attempt to improve the computational cost of solving such problems, including

- efficient numerical discretizations
- large-scale HPC implementations
- operator learning approaches
- quantum algorithms for linear systems

## References

1. Lions, J. L. *Optimal Control of Systems Governed by Partial Differential Equations.*
2. Hinze, M., Pinnau, R., Ulbrich, M., Ulbrich, S. *Optimization with PDE Constraints.*
3. Tröltzsch, F. *Optimal Control of Partial Differential Equations.* -->
