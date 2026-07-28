---
author: Anish Ghosh
title: "Classical Problems in Optimal Control — and a Quantum Solution"
date: 2026-03-05
image: "/img/blog/OptimalControl1.png"
categories: ["Mathematics"]
description: A short introduction to optimal control and PDE-constrained optimization.
math: true
---

Optimal control problems arise when we want to determine a **control variable**
that optimizes an objective function while satisfying physical or dynamical constraints.

These problems appear naturally in engineering, physics, economics and many areas
of applied mathematics.

<!--more-->
<!-- 
```bash
{{ if or .Params.math .Site.Params.math }}
{{ partial "math.html" . }}
{{ end }}
``` -->

{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}
<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}

In many applications the goal is to minimize a functional of the form

$$
\min_{u,x} J(u,x)
$$

subject to a constraint

$$
c(u,x) = 0
$$

where

- u represents the **state variable**
- x represents the **control variable**

In many scientific computing problems the constraint takes the form of a
**partial differential equation**

$$
A(x)u = f
$$

which leads to the class of **PDE-constrained optimization problems**.

### Why PDE-Constrained Optimization?

Many of the systems we care about most — the flow of air over a wing, the diffusion of heat through a turbine blade, the propagation of seismic waves through the earth, the spread of a disease through a population — are governed by partial differential equations. Whenever we want to *design*, *control*, or *infer* something about such a system, we are no longer just solving a PDE forward in time; we are searching for the input (a control, a boundary condition, a material parameter, a source term) that makes the resulting solution as close as possible to some desired behavior.

That search is inherently an optimization problem, and because the underlying physics must still be respected at every step, the PDE itself becomes a hard constraint c(u,x) = 0 rather than something we can ignore.

This is what makes the field necessary: naively perturbing a design and re-solving the PDE from scratch for every trial is far too expensive once the state variable lives in a high-dimensional discretized space (thousands to billions of unknowns), and directly differentiating through that discretization is usually intractable. Techniques like the adjoint method exist precisely to make these gradients affordable, which is what turns PDE-constrained optimization from a theoretical curiosity into a practical engineering tool.

In practice this framework underlies aerodynamic and structural shape optimization in aerospace and automotive design, optimal control of fluid flow and combustion, topology optimization of materials and structures, inverse problems in medical and seismic imaging, parameter estimation in climate and weather models, and even control problems in quantum systems — anywhere a physical process described by a PDE needs to be steered, designed around, or inferred from data.

### Reduced Objective: Optimizing Over x Alone

The constrained problem

$$
\min_{u,x} J(u,x) \qquad \text{subject to} \qquad c(u,x) = 0
$$

involves two sets of variables, but they are not independent: the constraint c(u,x) = 0 ties the state u to the control x. Assuming that for every admissible control x there exists a unique state u(x) solving c(u(x),x) = 0, the state is not a free variable at all — it is completely determined the moment x is chosen.

This lets us eliminate u from the optimization entirely. Define the reduced objective

$$
J(x) := J(u(x),x).
$$

Because u(x) already satisfies the constraint by construction, minimizing J(x) over x with no constraint at all is exactly equivalent to the original constrained problem:

$$
\min_{u,x} J(u,x) \qquad \text{s.t.} \qquad c(u,x)=0 \qquad \Longleftrightarrow \qquad \min_{x} J(x).
$$

This is why every optimization step from here on only ever updates the control x. The state u is never treated as an independent unknown: it is recovered by solving the state equation c(u,x) = 0 for the current x, and the objective is then differentiated only with respect to x. This reduction — from a constrained problem in (u,x) to an unconstrained problem in x alone — is exactly what makes the direct and adjoint methods below well posed, and is why both methods below compute a gradient with respect to x only.

### Direct Method

Consider the discretized problem with state variable u (n components), control variable x (n_x components), and constraint

$$
c(u,x) = 0.
$$

Assuming each control x admits a unique state u(x), differentiate the constraint with respect to each control component x_i using the chain rule:

$$
\frac{\partial c}{\partial u}\frac{\partial u}{\partial x_i} + \frac{\partial c}{\partial x_i} = 0.
$$

Writing A = ∂c/∂u for the state Jacobian (an n-by-n matrix), this rearranges into a linear system for the **sensitivity** ∂u/∂x_i:

$$
A \frac{\partial u}{\partial x_i} = -\frac{\partial c}{\partial x_i}, \qquad i = 1,\dots,n_x.
$$

Once ∂u/∂x_i is known, the gradient of the reduced objective J(x) := J(u(x),x) follows from the chain rule:

$$
\frac{\partial J}{\partial x_i} = \frac{\partial J}{\partial x_i} + \frac{\partial J}{\partial u}^{T} \frac{\partial u}{\partial x_i}.
$$

This is the **direct (sensitivity) method**: solve a linear system in A for every control variable x_i, then contract the result with ∂J/∂u.

**Why it is inefficient.** The matrix A does not depend on i, but the right-hand side -∂c/∂x_i does, so each of the n_x sensitivity equations must be solved separately. If solving one linear system of size n (the number of state variables) costs T_solve, the direct method costs

$$
n_x \cdot T_{\text{solve}}
$$

per optimization iteration. In realistic PDE-constrained problems n_x can itself be large — every mesh node, material parameter, or boundary value may be a control variable — so this cost grows linearly in n_x and quickly dominates. The direct method wastes effort re-deriving essentially the same linear solve, with only the right-hand side changing, once for every control variable.

### Adjoint Method

The adjoint method avoids solving one linear system per control variable by never computing ∂u/∂x_i at all. Introduce the Lagrangian

$$
\mathcal{L}(u,x,p) = J(u,x) + p^{T} c(u,x),
$$

where p (n components) is the **adjoint variable**, and choose p to satisfy the **adjoint equation**

$$
A^{T} p = \frac{\partial J}{\partial u}.
$$

This single linear system does not depend on i at all — it involves only A and ∂J/∂u, both already available at the current iterate. Substituting the adjoint equation into the direct-method gradient expression gives

$$
\frac{\partial J}{\partial u}^{T}\frac{\partial u}{\partial x_i}
= A^{T}p^{T}\frac{\partial u}{\partial x_i}
= p^{T} A \frac{\partial u}{\partial x_i}
= -p^{T}\frac{\partial c}{\partial x_i},
$$

using the sensitivity equation A ∂u/∂x_i = -∂c/∂x_i from the direct method. The reduced gradient therefore simplifies to

$$
\frac{\partial J}{\partial x_i} - p^{T}\frac{\partial c}{\partial x_i}, \qquad i = 1,\dots,n_x.
$$

The adjoint equation is solved **once** per optimization iteration, regardless of n_x, at a cost comparable to a single state solve. Each gradient component is then recovered from p using only an inner product with ∂c/∂x_i — a cheap vector operation, not another linear solve. The total cost per iteration drops from n_x · T_solve for the direct method to T_solve + O(n_x) for the adjoint method, which is why the adjoint method is the standard choice whenever the number of control variables is large.

### Where This Leaves Us

From the derivations above, the bottleneck in both the direct and adjoint methods is clear: everything comes down to solving large linear systems — the state equation, and either n_x sensitivity systems or a single adjoint system — and, in the adjoint case, computing inner products against the resulting vector to assemble the gradient. Linear solves and inner products are exactly the two primitives that quantum computers are known to accelerate: quantum linear system algorithms can solve certain sparse, well-conditioned systems exponentially faster than classical Krylov methods, and inner products between quantum states can be estimated directly using a swap test, without ever reconstructing the underlying vectors classically. Replacing the classical adjoint solve with a quantum one, and the inner products with swap-test estimates, gives a genuine speedup precisely where the classical method is most expensive.

We're actively working on exactly this — take a look at the project page: [https://theory-code.com/Quantum-Accelerated-Adjoint-Method-PDE-Constrained-Optimization/](https://theory-code.com/Quantum-Accelerated-Adjoint-Method-PDE-Constrained-Optimization/). The code and results are already up there — keep checking back, the arXiv writeup will be added soon.