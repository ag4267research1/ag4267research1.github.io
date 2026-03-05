---
title: "Optimal Control Problems"
date: 2026-03-05
draft: false
author: "Anish Ghosh"
categories: ["mathematics", "scientific-computing"]
math: true
---

Optimal control problems arise when we want to determine a **control variable**
that optimizes an objective while satisfying dynamical or physical constraints.
These problems appear naturally in engineering, physics, economics, and applied mathematics.

## Classical Formulation

A standard formulation can be written as

$$
\min_{u} J(u)
$$

subject to

$$
c(x,u) = 0
$$

where

- \(x\) represents the **state variable**
- \(u\) represents the **control variable**

## PDE-Constrained Optimization

In many applications the constraint takes the form of a **partial differential equation**

$$
A(u)x = f
$$

This leads to the class of **PDE-constrained optimization problems**.

## Adjoint Method

A common approach for computing gradients efficiently is the **adjoint method**.
Instead of differentiating the constraint explicitly, an adjoint equation is introduced.

This allows gradients of the objective functional to be computed with cost
comparable to solving the PDE itself.

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
