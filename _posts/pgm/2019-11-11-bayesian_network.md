---
layout:     post
title:      "Probabilistic Graphical Model"
subtitle:   "2-Bayesian Network(in progress)"
date:       2019-11-11 19:13:13
author:     "Ive Xu"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - pgm
    - machine learning
    - lecture notes
---

# Bayesian Network


## Naive Bayes Model

<img src="/img/post/image-20191027170652983.png" alt="image-20191027170652983" style="zoom:33%;" />

- Assumption: $\large (X_i \perp X_j  \vert  C)$
- $P(C, X_1, ..., X_n) = P(C) \prod_i^n P(X_i \vert C)$

## Graph and Distributions

> **I-map**
>
> $\mathcal{K}$ is a graph with independencies $I(\mathcal{K})$. $\mathcal{K}$ is an I-map of $P$ if $I(\mathcal{K}) \subseteq I(P)$ 

**<u>Factorization Theorem</u>**

Definition of a graph $\mathcal{G}$ in Bayesian Network to be $\large (X_i \perp NonDesc(X_i)  \vert  Pa_{X_i})$, that is $\large P(X_1, ..., X_n) = \prod_i^n P(X_i \vert Pa_{X_i})$ 



- **I-map $\rightarrow$ Factorization $(P)$**

![image-20191027171553215](/img/post/image-20191027171553215.png)

- **Factorization $(P) $ $\rightarrow$ I-map**

![image-20191027171606829](/img/post/image-20191027171606829.png)

## Bayesian Network Representation

* A Bayesian Network is a pair of $\{P, \mathcal{G}\}$ in which

  ​	\- $P$ factorize over $\mathcal{G}$

  ​	\- $P$ is specified as a set of CPDs associated with $\mathcal{G}$

* Distribution parameters representation

  ​	\- Joint distribution: $2^n$

  ​	\- Bayesian network (Conditional distribution): ~$n2^k$, $k$ bounded 

## Independencies in Graph

#### D-separation

**<u>Active Trail</u>**

<img src="/img/post/image-20191027173509327.png" alt="image-20191027173509327" style="zoom:33%;" />

![image-20191027173623624](/img/post/image-20191027173623624.png)

A trail is active (not-separated) given evidence (observed) $Z$ if 

* No nodes along the trail is in $Z$
* For every v-structure $X_{i-1} \rightarrow X_i \rightarrow X_{i+1}$, $X_i$ or one of its descendants is *observed*

> **d-separation**
>
> $X\ and\ Y$ are d-separated given $Z$, denote $d-sep_\mathcal{G}(X;Y \vert Z)$ if there is no active trail between any node $X$ and $Y$ given $Z$.

> **Global independencies**
>
> $I(\mathcal{G}) = \{(X \perp Y \vert Z): d-sep_\mathcal{G}(X;Y \vert Z) \}$



**<u>Minimal I-map</u>**

![image-20191027174111505](/img/post/image-20191027174111505.png)

Algorithm for building minimal I-map: the idea is to order the varaible then test the condition $(X_i \perp (X_1, ..., X_{i-1}-U'  \vert  U'))$, if true then set $U'$ to be $X_i$'s parents. In doing so, we see that different orderings may generate different network.

<img src="/img/post/image-20191027202501411.png" alt="image-20191027202501411" style="zoom:33%;" />

<img src="/img/post/image-20191027202515813.png" alt="image-20191027202515813" style="zoom:33%;" />

**<u>Perfect Map</u>**

![image-20191027174348169](/img/post/image-20191027174348169.png)

**<u>I-equivalence</u>**

Two graphs $\mathcal{G_1}\ and \ \mathcal{G_2} $ are I-equivalence if $I(\mathcal{G_1}) = I(\mathcal{G_2})$, that is the independencies encoded by the two graphs are the same.

$\mathcal{G_1}\ and \ \mathcal{G_2}$ are I-equivalence if and only if they have the same *skeleton* and the same set of *immortality* (v-structure).

<img src="/img/post/image-20191027201715962.png" alt="image-20191027201715962" style="zoom:33%;" />

## Causual effect 

<img src="/img/post/image-20191027202654178.png" alt="image-20191027202654178" style="zoom:50%;" />

What is the effect when we perform $do(X=x)$ ? 

$\rightarrow$  Remove all edges between $Y \rightarrow X$, $do(X=x)$ is a deterministic human intervention, it casuses all the casuasation to break down, therefore all links are removed.
