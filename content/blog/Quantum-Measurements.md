---
title: "Quantum Measurement: A Mathematical Overview"
date: 2026-03-21
draft: false
author: "A. Ghosh"
description:description: "This post develops the mathematics of quantum measurement, explains how measurement outcomes are modeled, and shows how the Stern–Gerlach experiment provides the basic intuition behind quantum tomography."
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



**Coming soon.**

This post will give a simple mathematical overview of quantum measurement for a single qubit. It will explain how a qubit is written as a vector in \(\mathbb{C}^2\) 
{{< math.inline >}} \( \mathbb{C}^2 \) {{</ math.inline >}}, how measurement in a basis produces outcomes from the squared sizes of the amplitudes, and why measurement changes the state. It will also use the Stern–Gerlach experiment to motivate the qubit model and the Bloch sphere to give an intuitive picture of single-qubit states and measurements.