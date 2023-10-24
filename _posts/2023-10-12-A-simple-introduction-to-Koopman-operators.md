---
layout: post
title: "A simple introduction to the Koopman operator"
date: 2023-10-13
featured-image: trace.png
---

The Koopman framework has become increasingly popular for studying dynamical systems. It was first introduced by Koopman and Von Neumann, who showed that each system can be associated with a linear operator {%cite von_neumann%}, {% cite bernard_koopman %}. The operator, when applied to complex-valued functions of the system states, results in the functions evaluated at a future state. Therefore, the dynamics can be studied in the function space instead of the state space. Thus, the Koopman operator framework is understood as studying the dynamics of observables instead of the dynamics of states. The Koopman operator is formulated as an operator that advances the observable’s value. Moreover, the linear nature of the operator makes it tractable for finite-dimensional matrix approximations. The Koopman framework addresses the challenge of dealing with non-linear dynamical systems. The classical geometric perspective allows analysis techniques to only be applied in the neighbourhood of fixed points, periodic orbits, and attractors of these non-linear systems by using local linearisations {% cite glendinning_1994 %}. The Koopman framework presents a global analysis of the system, thereby allowing for prediction and control away from fixed points and periodic orbits.

In this article, I introduce the Koopman operator and show how it allows for the study of non-linear dynamical systems by using an observable space where the dynamics becomes linear.

In functional analysis, the object of interests are functions and operators are defined as mathematical operations that act on a function. A function spaces $\mathcal{F}$ is a set of functions such as the space of continuous functions, the space of pointwise convergent functions, the space of bounded and integrable functions. An operator then is anything that maps a function $f \in \mathcal{F}$ to any other function $g \in \mathcal{F}$. In Koopman operator theory, these functions are also referred to as observables and the function spaces are called observable spaces.

$$
\newcommand{\koop}{\mathcal{K}}
$$

Given the state space $M$ and a discrete dynamical system $x_{n+1} = T(x_n)$ where $T:M\xrightarrow{}M$, $M \subseteq \mathbb{R}^D$ and $\mathcal{F}$ is the space of observables such that $f \in \mathcal{F}, f:M\xrightarrow{}\mathbb{C}$, the Koopman operator {% cite applied %}, $\koop: \mathcal{F} \xrightarrow{} \mathcal{F}$ is defined as

$$
\begin{equation}
\koop f(x_n) = f(T(x_n)),\ n \in \mathbb{N}.
\end{equation}
$$

Given the state space $M$ and a continuous dynamical system $\dot{x} = T(x)$ where $T:M\xrightarrow{}M$, $M \subseteq \mathbb{R}^d$ and $\mathcal{F}$ is the space of observables such that $f \in \mathcal{F}, f:M\xrightarrow{}\mathbb{C}$, the Koopman semigroup, $\{\koop^t\}_{t \in \mathbb{R}^+}$, $\koop^t: \mathcal{F} \xrightarrow{} \mathcal{F}$ is defined as

$$
\begin{equation}
\koop^t f(x) = f(T^t(x)),\ x \in M,
\end{equation}
$$

where $T^t:M\xrightarrow{}M$ is the flow of the system. The generator of the Koopman semigroup, $\mathcal{A}_\koop: \mathcal{F} \xrightarrow{} \mathcal{F}$ is defined as

$$
\begin{equation}
\mathcal{A}_\koop f = \lim_{t \to 0} \dfrac{\koop^t f - f}{t}.
\end{equation}
$$

The Koopman operator transfers the dynamics from the state space to the observable/function space. In the observable space, the dynamics becomes linear. This can be seen in the case of discrete systems by

$$
[\koop(af_1 + bf_2)](x_n) = (af_1 + bf_2)(T(x_n)) = af_1(T(x_n)) + bf_2(T(x_n)) = a [\koop f_1](x_n) + b[\koop f_2](x_n)
$$

and in the case of continuous systems by

$$
[\koop^t(af_1 + bf_2)](x) = (af_1 + bf_2)(T^t(x)) = af_1(T^t(x)) + bf_2(T^t(x)) = a [\koop^t f_1](x) + b[\koop^t f_2](x)
$$

Additionally for continuous systems, the flow in the observable space is induced by $\koop^t$ and given by

$$
\begin{equation}
\koop^t = e^{\mathcal{A}_\koop t},
\end{equation}
$$

where $\mathcal{A}_{\koop}$ is the Koopman generator.

Therefore we see, that the application of $\koop^t$ to an observable $f$ at state $x$ advances the value of the observable $f$ at state $T^t(x)$ for continuous systems. For discrete systems, the application of operator $\koop$ to an observable $f$ at state $x_n$ advances the value of the observable $f$ at state $x_{n+1}$.

Now that we know that the Koopman operator is a linear operator that incudes linear dynamics in the observable space, we can study the eigenfunctions and the eigenvectors of the Koopman operator.

The eigenfunctions and eigenvalues of the Koopman operator are defined by the eigen equations. For the discrete system,

$$
\begin{equation}
    \label{eq: eigen_rls_discrete}
    (\koop \phi) (x_n) = \lambda \phi (x_n),\ n \in \mathbb{N}.
\end{equation}
$$

And for the continuous system by

$$
\begin{equation}
    \label{eq: eigen_rls_continuous}
    (\mathcal{A}_\koop \phi) (x) = \lambda \phi (x).
\end{equation}
$$

Then, the eigen equation for $\koop^t, t \geq 0$ is

$$
\begin{equation}
(\koop^t \phi) (x) = e^{\lambda t} \phi (x).
\end{equation}
$$

As dynamical systems are defined on state spaces and not on function spaces, to study them via functions requires a full-state observable function $g(x) = x \in \text{span}\\{f\\}_{f \in \mathcal{F}}$. Then

$$

\begin{align*}
& x = \sum_{i=1}^n C_i(x) \phi_i(x)\\
\implies & T(x) = g(T(x)) = [\koop g](x) = \sum_{i=1}^n \lambda_i C_i(x) \phi_i(x).
\end{align*}
$$

The terms $C_i$ are called the Koopman modes and represent the projection of the full- state observable onto the eigenfunctions. The observable dynamics and the state space dynamics can be connected via the full state observable. Additionally, the system trajectories can be computed using the Koopman eigenfunctions and eigenvalues.

#### Rotation of a circle

We consider an example with the dynamical system $T: M\xrightarrow{}M$ on $M = [0,1)$.

$$
T(x) = x+w\ \text{mod}\ 1.
$$

This system is isomorphic to rotation on a circle.

If we consider the functions $\phi_n(x) = e^{i 2 \pi n x}$, then

$$
[\koop \phi_n](x) = \phi_n(T(x)) = e^{i2\pi n(w+x)} = e^{i2\pi nw }.  e^{i2\pi nx}=  e^{i2\pi nw}\phi_n(x).
$$

Therefore $\phi_n$ is a Koopman eigenfunction with eigenvalue $\lambda_n = e^{i2\pi nw}$. Now we consider an observable $f \in \mathcal{F}$ that lies in the span of these eigenfunctions $\\{\phi_n\\}_{n \in \mathbb{N}}$. As the trignometric polynomials are dense in $L^1(M)$, this is expected.Then

$$
f(x) = \sum_{n \in \mathbb{Z}} \hat{f}(n) e^{i 2\pi nx}.
$$

where $\hat{f}(n)$ are the Fourier coefficients. Then the dynamics of observable $f$ is given by

$$
[\koop^m f](x) =  \sum_{n \in \mathbb{Z}} \hat{f}(n) \lambda_n^m e^{i 2\pi nx} =
\sum_{n \in \mathbb{Z}} \hat{f}(n) e^{i2\pi mnw} e^{i 2\pi nx},\ m \in \mathbb{N}.
$$

As we have seen in the example, the Koopman framework can be used to study non-linear dynamical systems with a linear framework. Practically, the Koopman operator is numerically approximated using algorithms such as Dynamic mode decomposition{%cite Tuetal2014%} and Extended dynamic mode decomposition {%cite williams_edmd%}. These algorithms are data-driven, in the sense that an explicit formulation of the system is not required to approximate the operator.

References:

{% bibliography %}
