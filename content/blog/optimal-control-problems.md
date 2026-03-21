---
author: Anish Ghosh
title: Optimal Control Problems
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
\min_{u} J(u)
$$

subject to a constraint

$$
c(x,u) = 0
$$

where

- \(x\) represents the **state variable**
- \(u\) represents the **control variable**

In many scientific computing problems the constraint takes the form of a
**partial differential equation**

$$
A(u)x = f
$$

which leads to the class of **PDE-constrained optimization problems**.

### Adjoint Method

A common technique for computing gradients efficiently is the **adjoint method**.
Instead of differentiating the PDE constraint directly, an adjoint equation is introduced.

This allows gradients of the objective functional to be computed with a cost
comparable to solving the PDE itself.

### Examples

{{< math.inline >}}
<p>
Example of inline math appearing in optimal control:
\( \nabla J(u) = \frac{\partial J}{\partial u} \)
</p>
{{</ math.inline >}}

Block equation example:

$$
\mathcal{L}(x,u,\lambda) =
J(x,u) + \lambda^{T} c(x,u)
$$

where \( \lambda \) represents the **adjoint variable**.