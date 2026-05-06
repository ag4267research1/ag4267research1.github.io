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


## What is a Qubit?

A qubit, or quantum bit, is the basic unit of information in quantum computing. In classical computing, a bit can only be in one of two states: {{< math.inline >}}0{{</ math.inline >}} or {{< math.inline >}}1{{</ math.inline >}}. A qubit is different because it can be written as a combination of two basis states, usually denoted as {{< math.inline >}}|0\rangle{{</ math.inline >}} and {{< math.inline >}}|1\rangle{{</ math.inline >}}.

Mathematically, a general qubit state is written as

$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle
$$

Here, {{< math.inline >}}\alpha{{</ math.inline >}} and {{< math.inline >}}\beta{{</ math.inline >}} are complex numbers called probability amplitudes. These amplitudes determine the probabilities of measuring the qubit as either {{< math.inline >}}0{{</ math.inline >}} or {{< math.inline >}}1{{</ math.inline >}}.

The probability of measuring the state {{< math.inline >}}|0\rangle{{</ math.inline >}} is

$$
P(0) = |\alpha|^2
$$

and the probability of measuring the state {{< math.inline >}}|1\rangle{{</ math.inline >}} is

$$
P(1) = |\beta|^2
$$

Since the measurement must produce either {{< math.inline >}}0{{</ math.inline >}} or {{< math.inline >}}1{{</ math.inline >}}, the probabilities must add up to one:

$$
|\alpha|^2 + |\beta|^2 = 1
$$

This condition is called normalization.

A simple example of a qubit in superposition is

$$
|\psi\rangle = \frac{1}{\sqrt{2}}|0\rangle + \frac{1}{\sqrt{2}}|1\rangle
$$

In this case, the probability of measuring {{< math.inline >}}0{{</ math.inline >}} is

$$
\left|\frac{1}{\sqrt{2}}\right|^2 = \frac{1}{2}
$$

and the probability of measuring {{< math.inline >}}1{{</ math.inline >}} is also

$$
\left|\frac{1}{\sqrt{2}}\right|^2 = \frac{1}{2}
$$

So, when this qubit is measured, there is a {{< math.inline >}}50\%{{</ math.inline >}} chance of getting {{< math.inline >}}0{{</ math.inline >}} and a {{< math.inline >}}50\%{{</ math.inline >}} chance of getting {{< math.inline >}}1{{</ math.inline >}}.

The important idea is that a qubit is not simply “both 0 and 1” in a classical sense. Instead, it is a quantum state described by probability amplitudes. Quantum algorithms work by carefully changing these amplitudes so that, after measurement, the correct answer becomes more likely.