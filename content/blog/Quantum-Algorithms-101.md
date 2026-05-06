---
title: "Quantum Computing Basics: Qubits, Superposition, and Measurement"
date: 2026-03-21
draft: false
author: "A. Ghosh"
description:description: "Before diving into quantum algorithms, we need to understand the basic building blocks of quantum computing. This post introduces qubits, superposition, probability amplitudes, measurement, and entanglement in an intuitive way. The goal is to build the foundation needed to understand how quantum algorithms manipulate quantum states and why they can behave differently from classical algorithms."
image: "/img/blog/Quantum_Computing/Measurement/QM1.png"
categories: ["Mathematics"]
tags: ["quantum algorithms"]
math: true
---

{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}
<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}

## Single Qubit

In classical computing the basic unit of information is a bit. A bit can be only in one of the two states either zero or one and therefore can be physically implemented by a two state device. A qubit is the basic unit of information in quantum computing.
{{< math.inline >}}
Unlike a bit, a qubit is not restricted to only \(0\) or \(1\) before measurement.
{{</ math.inline >}}
{{< math.inline >}}
The vectors \(|0 \rangle = \begin{bmatrix}
1 \\
0
\end{bmatrix}\) and \(|1\rangle = \begin{bmatrix}
0 \\
1
\end{bmatrix} \)
{{</ math.inline >}}

{{< math.inline >}}
<p>
The computational basis vectors are
\( |0\rangle = \left[\begin{smallmatrix} 1 \\ 0 \end{smallmatrix}\right] \)
and
\( |1\rangle = \left[\begin{smallmatrix} 0 \\ 1 \end{smallmatrix}\right] \).
</p>
{{</ math.inline >}}




The two computational basis states are

$$|0\rangle =
\begin{bmatrix}
1 \\
0
\end{bmatrix},
\qquad
|1\rangle =
\begin{bmatrix}
0 \\
1
\end{bmatrix}.$$
