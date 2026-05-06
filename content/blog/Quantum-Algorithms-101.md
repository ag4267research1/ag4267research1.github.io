---
title: "Quantum Computing Basics: Qubits, Superposition, and Measurement"
date: 2026-03-21
author: "A. Ghosh"
description: "Before diving into quantum algorithms, we need to understand the basic building blocks of quantum computing. This post introduces qubits, superposition, probability amplitudes, measurement, and entanglement in an intuitive way. The goal is to build the foundation needed to understand how quantum algorithms manipulate quantum states and why they can behave differently from classical algorithms."
image: "/img/blog/Quantum_Computing/Measurement/QM1.png"
categories: ["Mathematics", "Computing"]
tags: ["quantum algorithms", "qubits", "superposition"]
math: true
---

## Single Qubit

In classical computing, the basic unit of information is a bit. A bit can only be in one of two states, either zero or one, and therefore it can be physically implemented by a two-state device.

A qubit is the basic unit of information in quantum computing. Unlike a bit, a qubit is not restricted to only $0$ or $1$ before measurement.

The two computational basis states are written as $|0\rangle$ and $|1\rangle$.

The two computational basis states are

$$
|0\rangle =
\begin{bmatrix}
1 \\\\
0
\end{bmatrix},
\qquad
|1\rangle =
\begin{bmatrix}
0 \\\\
1
\end{bmatrix}.
$$

A general single-qubit state is written as

$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle.
$$

Here, $\alpha$ and $\beta$ are complex numbers called probability amplitudes.

Using column-vector notation, the same qubit can be written as

$$
|\psi\rangle =
\begin{bmatrix}
\alpha \\\\
\beta
\end{bmatrix}.
$$

For the qubit to be physically valid, the amplitudes must satisfy the normalization condition

$$
|\alpha|^2 + |\beta|^2 = 1.
$$

The probability of measuring $0$ is $|\alpha|^2$, and the probability of measuring $1$ is $|\beta|^2$.

Therefore,

$$
P(0) = |\alpha|^2,
\qquad
P(1) = |\beta|^2.
$$