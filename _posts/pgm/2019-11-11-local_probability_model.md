---
layout:     post
title:      "Probabilistic Graphical Model"
subtitle:   "4-Local Probability Model (in progress)"
date:       2019-11-11 19:43:13
author:     "Ive Xu"
header-img: "img/home-bg-art.jpg"
catalog: true
tags:
    - pgm
    - machine learning
    - lecture notes
---

# Local Probability Model


## Tabular CPDs

table-CPDs also known as *conditional probability tables (CPTs)*, the main idea is to just record $P(X \vert Pa_X)$ in a table in such a way that $\sum_{x \in val(X)} P(x \vert Pa_X) = 1$. 

* Advantage: save memory space, inherited representation from Bayesian Network
* Disadvantage: the number (space) grows exponentially that is $O( \vert Val(Pa_X) \vert \cdot \vert Val(X) \vert )$

## Deterministic CPDs

Let not view CPDs as tables but as a function of given $Pa_x$ and $x$. When the the variable $X$ is a ***deterministic*** function  of its parent $Pa_X$, e.g. $X = Y + X,\ X = sin(y + e^z) ...$ or

<img src="/image/post/image-20191027143531886.png" alt="image-20191027143531886" style="zoom:30%;" />

## Context-Specific CPDs

Definition of context-specific independent is that for a set of variable $C$ with $c \in Val(C)$, $X$ and $Y$ are *contextually independent* given $Z$ denoted by $(X \perp_c Y  \vert  Z, c)$ if $P(X, Y \vert  Z, c) = P(X \vert Z, c) \ whenever P(Y, Z, c) > 0$. To put it simple, we say that if some particular values of $C$ is known, then $X\ and\ Y$ are independent given $Z$. For each $c \in Val(C)$, the contextual independencies might be *different*.

## Tree CPDs
(...)

## Rule CPDs
(...)

## Noisy-Or Model

Motivated example, The bank data center will run down if **any one** of the computers run down at the same time.

* Define $f_1\ to\ f_k$ as noisy-or parameters (failure rate of one computer), and $f_0$ as leak probability

* Noisy-or model 

  * $P(F = false) = (1-f_0)\prod_1^k (1-f_i)$
  * $P(F = true) = 1 - (1-f_0)\prod_1^k (1-f_i)$

* BN2O (Bayesian Network to Oberservation?)

  * Extension from Noisy-or model & Naive Bayes

    <img src="/image/post/image-20191027204834983.png" alt="image-20191027204834983" style="zoom:20%;" />

* Other noisy model

  * Noisy-and model
  * Noisy-max model

## Generalized Linear Model

<img src="/image/post/image-20191027205507768.png" alt="image-20191027205507768" style="zoom:25%;" />

* We focus on models that define $P(Y \vert X_1, ...X_k)$ , where now consider all variables are binary

* Assume $f(X_1, ..., X_k) = w_0 + \sum_i^k w_i X_i$

* Consider to threshold $f(X_1, ..., X_k) , if\ f(X_1, ..., X_k)> 0\ then\ Y=1,\ otherwise\ Y=0$

* Introduce *sigmoid* or *logit* function $\large sigmoid(z)={e^z \over 1+e^z}$

* We get the *logistic CPDs* that is $P(Y^1 \vert X_1, ..., X_k) = sigmoid(w_0 + \sum_i^kw_iX_i)$

* *log odds* (log CPD ratio) $O(X) = {P(y^1 \vert X_1, ..., X_k) \over P(y^0 \vert X_1, ..., X_k)} = {{e^Z \over{1+e^Z}} \over {1 \over{1+e^Z}}} = e^Z$

* If we to make decision then if $e^Z > 1 \Rightarrow Y=1,\ otherwise\ Y=0$

  <img src="/image/post/image-20191027155351054.png" alt="image-20191027155351054" style="zoom:25%;" />

**<u>Multivalued-variables</u>**

$Y$ is an $m$ valued random variable with $k$ parents $X_1, ..., X_k$, the CPDs is a *multinomial logistic* such that 

$\Large P(y^j \vert X_1, ..., X_k) = {exp(w_{j,0} + \sum_i^k w_{j,i}X_i) \over \sum_{j'=1}^mexp(w_{j',0} + \sum_i^k w_{j',i}X_i)}$

## Linear Gaussian Model

$Y$ is an continuous random variable with continuous parents $X_1, ..., X_k$. $Y$ is a *linear Gaussian* model with parameters $\beta_0, ..., \beta_k\ and\ \sigma^2$ such that $P(Y \vert X_1,...,X_k)=\mathcal{N}(\beta_0+ \beta_1x1+...+\beta_kx_k,\sigma^2)$

* Binomial distribtuion
  * $P(Y \vert X) = sigmoid(w_0 + \sum_i^kw_ix_i)$ 
* Poisson distribtuion
  * $P(Y \vert X) = \lambda^ke^{-\lambda} /k!\ ,\ \lambda = w_0 + \sum_i^kw_ix_i$

## Hybrid Model (Discrete and Cont.)

## BN Model Representation

<img src="/image/post/image-20191027205621413.png" alt="image-20191027205621413" style="zoom:33%;" />

* **Variable**: *circle*, observed variable marked as *shaded*
* **Relation**: edges with and without direction
* **Parameters**: without *circle*
* **Square box**: number of repeated representation or sample size
