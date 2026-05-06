---
title: "Quantum Computing Basics: Qubits, Superposition, and Measurement"
date: 2026-03-21
draft: false
author: "A. Ghosh"
description:description: "Before diving into quantum algorithms, we need to understand the basic building blocks of quantum computing. This post introduces qubits, superposition, probability amplitudes, measurement, and entanglement in an intuitive way. The goal is to build the foundation needed to understand how quantum algorithms manipulate quantum states and why they can behave differently from classical algorithms."
image: "/img/blog/Quantum_Computing/Measurement/QM1.png"
categories: ["Computing"]
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

A single qubit is the basic mathematical object used to represent quantum information.

{{< math.inline >}}
<p>
A single qubit lives in a two-dimensional complex vector space, written as \( \mathbb{C}^2 \).
</p>
{{</ math.inline >}}

The two standard basis states are

$$
|0\rangle =
\begin{bmatrix}
1 \\
0
\end{bmatrix},
\qquad
|1\rangle =
\begin{bmatrix}
0 \\
1
\end{bmatrix}.
$$

A general single-qubit state is written as

$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle.
$$

{{< math.inline >}}
<p>
Here, \( \alpha \) and \( \beta \) are complex numbers, so \( \alpha, \beta \in \mathbb{C} \).
</p>
{{</ math.inline >}}

Using vector notation, the qubit can be written as

$$
|\psi\rangle =
\begin{bmatrix}
\alpha \\
\beta
\end{bmatrix}.
$$

{{< math.inline >}}
<p>
The values \( \alpha \) and \( \beta \) are called probability amplitudes.
</p>
{{</ math.inline >}}

For the qubit to represent a valid quantum state, it must satisfy the normalization condition

$$
|\alpha|^2 + |\beta|^2 = 1.
$$

{{< math.inline >}}
<p>
This means the total probability of all possible measurement outcomes must equal \( 1 \).
</p>
{{</ math.inline >}}

If the qubit is measured in the computational basis, then the probability of measuring the state is given by

$$
P(0) = |\alpha|^2,
\qquad
P(1) = |\beta|^2.
$$

Therefore,

$$
P(0) + P(1) = |\alpha|^2 + |\beta|^2 = 1.
$$

{{< math.inline >}}
<p>
After measurement, the qubit becomes \( |0\rangle \) with probability \( |\alpha|^2 \), or it becomes \( |1\rangle \) with probability \( |\beta|^2 \).
</p>
{{</ math.inline >}}

A single qubit is the basic mathematical object used to represent quantum information.

{{< math.inline >}}
<p>
A single qubit lives in a two-dimensional complex vector space, written as \( \mathbb{C}^2 \).
</p>
{{</ math.inline >}}

The two standard basis states are

$$
|0\rangle =
\begin{bmatrix}
1 \\
0
\end{bmatrix},
\qquad
|1\rangle =
\begin{bmatrix}
0 \\
1
\end{bmatrix}.
$$

A general single-qubit state is written as

$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle.
$$

{{< math.inline >}}
<p>
Here, \( \alpha \) and \( \beta \) are complex numbers, so \( \alpha, \beta \in \mathbb{C} \).
</p>
{{</ math.inline >}}

Using vector notation, the qubit can be written as

$$
|\psi\rangle =
\begin{bmatrix}
\alpha \\
\beta
\end{bmatrix}.
$$

{{< math.inline >}}
<p>
The values \( \alpha \) and \( \beta \) are called probability amplitudes.
</p>
{{</ math.inline >}}

For the qubit to represent a valid quantum state, it must satisfy the normalization condition

$$
|\alpha|^2 + |\beta|^2 = 1.
$$

{{< math.inline >}}
<p>
This condition means that the total probability of all possible measurement outcomes must equal \( 1 \).
</p>
{{</ math.inline >}}

If the qubit is measured in the computational basis, then the probability of measuring the state \( |0\rangle \) is

$$
P(0) = |\alpha|^2.
$$

The probability of measuring the state \( |1\rangle \) is

$$
P(1) = |\beta|^2.
$$

Therefore,

$$
P(0) + P(1) = |\alpha|^2 + |\beta|^2 = 1.
$$

After measurement, the qubit becomes one of the basis states. It becomes \( |0\rangle \) with probability \( |\alpha|^2 \), or it becomes \( |1\rangle \) with probability \( |\beta|^2 \).