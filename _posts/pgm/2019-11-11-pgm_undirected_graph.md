---
layout:     post
title:      "Probabilistic Graphical Model"
subtitle:   "2-Undirected Graph (in progress)"
date:       2019-11-11 14:43:013
author:     "Ive Xu"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - pgm
    - machine learning
    - lecture notes
---

# Undirected Graph

[TOC]

## Reduce Markov Network

The conditioning on a context $u$ of a markov network is just to eliminate the **node** and all the **edges**.

<img src="/img/post/image-20191025165124585.png" alt="image-20191025165124585" style="zoom: 50%;" />

## Markov Network Independencies 

* Notion of independencies in MN is the influence "**flow**", if $X \ and \  Y$ are blocked by some nodes $Z$, then $X \perp Y | \ Z$ 

> **Active path**: a path $X_1 - ...-X_k$ be a path is active given $Z$ if *none* of $X_i$ is in $Z$, mean that nodes along the path is *unobserved*. 

> **Separation**: $sep_\mathcal{H}(X;\ Y|\ Z)$ if there is no active path between any nodes in $X$ and $Y$ given $Z$

> **Global independencies**: $I(\mathcal{H}) = \{ X\ \perp Y|\ Z\ :\ sep_\mathcal{H}(X;Y|Z) \}$ 

* digession: if $X$ and $Y$ are separated given $Z$ in $\H$ then we conclude that $X \perp Y | Z$  
* Monotonic independencies:  if $sep_{\mathcal{H}}(X;Y|Z),\ Z' \subseteq Z$, then $sep_{\mathcal{H}}(X;Y|Z')$

>  **<u>Theorem</u>**
>
> (1) if $P$ is a Gibbs distribution that factorizes over $\mathcal{H}$ $\Rightarrow$ $\mathcal{H}$ is an I-map for $P$. conversely, 
>
> (2) (*Hammersley-Clifford Theorem*) If $P$ is a *positive* distribtuion over $X$ and $\mathcal{H}$ is an I-map for $P$ $\Rightarrow$ $P$ is a Gibbs distribtution factorizes over $\mathcal{H}$. 

### Local Independencies vs Global Independencies

If two variables are *directly linked*, their pairwise correlation is presented in the potentials; if two variables are *not directly linked*, then there must be some way that $X$ and $Y$ are conditionally independent given some other variables $Z$. 

> **Pairwise Independencies**
>
> $I_p(\mathcal{H}) = \{(X \ \perp Y|\ \mathcal{X} - \{X, Y\}): X-Y \notin \mathcal{H}\}$ 

This leads to one interesting implication that for a set of variables $X$, they only depend on their immidiate neighbours $Y$ such that $X - Y$, which form a **Markov blanket** $MB_\mathcal{H}(U)$.  Then the **Local independencies** can be defined as below

> **Markov Blanket**
>
> A set $U$ is a Markov blanket of $X$ in a distribution $P$ if $X \notin U$ and if $U$ is a minimal set of Markov blanket nodes such that $(X \perp \mathcal{X} - \{ X\} - U| U) \in I(P)$, that is these independencies must be captured by $P$.

> **Local independencies of MN**
>
> $I_l(\mathcal{H}) = \{ (X \perp \mathcal{X} - \{X\} - MB_\mathcal{H}(X)| MB_\mathcal{H}(X): X \in \mathcal{X})\}$ that is $X$ is independent with the rest of nodes given its immidiate neighbours $MB_\mathcal{H}(X)$.

**\*\*** ***Generally, the relationship is $I_p(\mathcal{H}) << I_l(\mathcal{H}) << I(\mathcal{H})$*** 

## MN Parameterization

<img src="/img/post/image-20191025210237613.png" alt="" style="zoom:50%;" />


The graph structure does not reveal all structure of the Gibbs distribution whether the factors parameterization invlove which maximal cliques or subset thereof, as shown in the figure above. An alternative way to represent this structure is done with a ***Factor Graph*** that contains two types of variables: *variable nodes* (usual nodes) and *factor nodes* (corresponds to factor over nodes) 

### Log-Linear Model

$\large{ \boxed{\Psi(D) = \prod \epsilon_i(D_i) \Rightarrow \phi(D) = exp(\sum - \epsilon_i(D))}}$  

$\ where\ \epsilon_i(D) = -ln \phi(D)$ is often called *energy function*. Then, we have that any Markov network can be converted to a logarithmic representation as $\large P(X_1, ..., X_n) \propto \ exp[\sum-\epsilon_i(D)]$ 

**<u>Log-Linear Model</u>**

Let define feature $f(D)$ to be a function from $val(D)$ to $\mathbb{R}$, that is simply a factor *without* nonnegativity requirements and here we are interested in the *indicator function* which take only $0, 1$ value.

> **Log-linear Model**
>
> $P$ is a log-linear model associated with 
>
> * A set of features $\mathcal{F} = \{F_1(D_1), ..., F_k(D_k)\}$, where each $D_i$ is a complete subgraph
> * A set of weights $w_1, ..., w_k$ 
>
> $\large P(X_1, ..., X_n) = {1 \over Z} exp[-\sum_{i=1}^{k}w_i f_i(D_i)]$

**<u>Ising Model</u>**

* binary valued-variables $X_i \in \{ +1, -1\}$
* $w_{i,j}$ encodes interactions between two variables(atoms), $w_{i,j} = 0$ no interaction
*  $u_i$ encodes individual potentials; the energy function is  $\large P(\xi) = {1 \over Z} exp(-\sum_{i<j} w_{i,j}x_ix_j - \sum_i u_ix_i)$

### Conditional Random Field

> A **Conditional Random Field** is an undirect graph $\mathcal{H}$ whose nodes correspond to $X \cup Y$ and a set of factors $\phi(D_i)\ s.t\  D_i \nsubseteq X$; the network encode below distribution
>
> $\large{P(Y|X) = {1 \over Z(X)} \widetilde{P}(Y, X) \\ \widetilde{P}(X, Y) = \prod_i \phi_i(D_i) \\ Z(X) = \sum_X \widetilde{P}(X,Y)}$
>
> That is two variables in $\mathcal{H}$ are connected by an (undirected) edge whenever they appear together in the scope of some factor.

Example of CRF

<img src="/img/post/image-20191027141629782.png" alt="image-20191027141629782" style="zoom:50%;" />

<img src="/img/post/image-20191027142109138.png" alt="image-20191027142109138" style="zoom:40%;" />

Models for text analysis based on Linear CRF

<img src="/img/post/image-20191027142243310.png" alt="image-20191027142243310" style="zoom:25%;" />

