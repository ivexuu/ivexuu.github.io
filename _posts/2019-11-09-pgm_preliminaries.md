---
layout:     post
title:      "PGM Preliminaries"
subtitle:   " \"Hello World, Hello Blog\""
date:       2019-11-09 23:13:013
author:     "Ive Xu"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - pgm
    - Meta
---

# PGM Preliminaries

## Probability

**<u>Bayes Rule</u>** : $\large P(A|B) = {P(B|A)P(A) \over P(B)}$

**<u>Chain Rule</u>**: $P(X_1, ..., X_k) = P(X_1)P(X_2|X_1)...P(X_k|X_1, ..., X_{k-1})$

**<u>Independence</u>** $P(A \cap B) = P(A)P(B)$ or $P(A|B)=P(A)$

**<u>Conditional Independence</u>** for an event $C$, for **all** $x \in Val(X), y \in Val(Y),\ z \in Val(Z)$ denoted $P \vDash (X \perp Y|Z)$, $P(X=x|Y=y,Z=z) = P(X=x|Z=z)$, $Z$ is said to be **observed**. We also have $P(X, Y|Z) = P(X|Z)P(Y|Z)$

* Decomposition: $\large (X \perp Y , W | Z) \Rightarrow (X \perp Y | Z)$
* Weak Union: $\large (X \perp Y,W|Z) \Rightarrow (X \perp Y| W, Z)$
* Contraction: $\large (X \perp W|Z, Y)\ \&\ (X \perp Y|Z) \Rightarrow (X \perp W,Y|Z)$

## Graph(simplified)

**<u>Graph</u>** a set of nodes and edges $\mathcal{K} = (\mathcal{X}, \mathcal{E})$

**<u>Boundary</u>** is the union of parents and neighbours $Pa_X\ \cup\ Nb_X$

**<u>Induced subgraph</u>**: a subgraph that contains some subset of nodes $X$ and ***all*** the edges appears in the $\mathcal{X}$ with the the subset of nodes $X$.

**<u>Upward closure</u>**: a subset of nodes $X \in \mathcal{X}$ is upwardly closed in $\mathcal{K}$ if, for any $X \in \mathcal{X}$ , $Boundary_X \subset X$. The upward closure of $X$ is the *minimal upwardly closed subset* $Y$ that contains X.

<img src="/img/post/image-20191027163342019.png" alt="image-20191027163342019" style="zoom:33%;" />

**<u>Path</u>** $X_i \rightarrow X_{i+1}\ or\ X_i-X_{i+1}$ , all nodes in a path are distinct

**<u>Trail</u>** all edges in a trail are distinct

**<u>Chordal Graph</u>** for every loop, there is an edge between $X_i, X_j$ for every *two non-cosecutive* nodes

<img src="/img/post/image-20191027170503828.png" alt="image-20191027170503828" style="zoom:25%;" />

