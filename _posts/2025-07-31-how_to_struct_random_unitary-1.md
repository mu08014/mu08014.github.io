---
layout: post
title:  "How to Struct Random Uniatry 1"
date:   2025-07-31 18:10:00 +0900
categories: 
  - study
description: >
  How to efficiently struct Pseudo Random Unitary(PRU)?
hide_description: true
permalink: '/:categories/:year/:month/:day/:title/'
related_posts:
  -
sitemap: false
---

Pseudorandom Uniatry의 정의는 [JLS18](https://arxiv.org/pdf/1711.00385)에서 제시되었다. 여러 후보들이 제시되었으나, Quantum Secure One-way function이 존재할 때 Pseudorandom Uniatry의 존재성은 오랜기간 Open Question이였다. 그러다 2024년 Fermi Ma와 Robert Huang은 [MH24](https://dl.acm.org/doi/abs/10.1145/3717823.3718254)논문에서 모든 정의의 조건을 만족하는 Unitary를 발견함으로써 Question을 close 하였다. 본 글은 위 논문의 Pseudorandom Uniatary의 Construction 방법에 대해서 설명해 보고자 한다. 논문에서는 기존 Pseudorandom이 정의되는 Adversary(BQP)의 계산적 능력 범의보다 더 강한 계산적 능력을 가졌을 때도 깨지지 않는 PRU 형태를 보였으나, 본 글에서는 기존에서 가능한 PRU까지만 설명할 것이다. 엄밀한 방법론과 형태는 논문을 직접 읽는 것을 권한다.

## Introduction

Random Unitary (Haar random unitary)는 Quantum information theory, quantum algorithm, quantum leartning 등 여러 분야에서 중요한 역할을 한다. 그러나, 이러한 Unitary를 구현하는건 물리적으로 매우 어렵고, exponential한 circuit depth가 필요하다고 알려져 있다. 따라서, Random Unitary를 잘 사용해 보기 위해 여러 방법론이 제시되었는데, 그 중 기존까지 많이 사용되던 방법이 Unitary t-design이다. 이 방법은 Random Unitary에서 통계적인 특성을 모사한다. 즉, 이렇게 만들어진 유니터리 ensemble은 t-moment까지 통계적으로 구분불가능함을 보장한다. 그런데, 비교적 최근 Pseudorandom Unitary의 개념이 제시되었다. 이 개념은 고전암호에서 많이 사용되던 Pseudorandom generator에서 아이디어를 얻었다. 고전적인 Pseudorandom은 관측자의 계산 능력이 "효율적"이라고 제한되어 있으면, 실제 랜덤한 분포와 주어진 키값을 통해 만들어진 결정론적인 숫자 분포는 구분 불가능하고, 이러한 분포는 존재할 수 있다.

예를 들어보자. 1~34의 자연수에서 랜덤한 값을 샘플링하는것을 구현하고자 한다. 그러나, 이 숫자들의 랜덤한 분포를 자연에서 찾기는 쉽지 않다. 따라서, 먼저 소수 5와 7을 곱해서 35를 만든다. 그리고 초기값을 무작위로 하나 정한다. 여기서는 9라고 해보자. 그러면, 9를 1~4중 하나의 숫자만큼 제곱하고 modular 35 연산을 취한다. 즉, 예를들어 4을 뽑았다고 하면 9의 네제곱을 취하고 mod 35를 취한다. 그럼 16이라는 값이 나온다. 다시 이 16에서 1~4중 하나의 숫자만큼을 제곱하고 modular 35 연산을 취한다. 2를 뽑았다고 하자. 16의 제곱을 하고 modular 35 연산을 취한다. 그럼 11이라는 값이 나온다. 이 과정을 계속 반복한다.

{9, 16, 11, ...}

이렇게 생성되는 숫자들의 분포는 1~34 범위의 값을 가지고, 관측자의 계산 능력이 제한되어 있다면, 실제 랜덤분포와 구분할 수 없다는데 Pseudo-random의 개념이다. 여기서 아이디어를 얻어 state 및 unitary에 대해서도 계산적 능력이 제한되어 있을 때 실제 결정론적인 state 및 unitary와 Haar random state 및 Haar random Unitary를 구분할 수 없다는 "Quantum Pseudorandom State, Unitary"를 정의하였다. 물론 여기서는 Quantum Machine의 계산 능력을 가진 Adversary에 대해서 깨지지 않는다고 가정해야 한다. 이에 대한 암호학적 정의가 Quantum secure one-way funciton이다. state의 경우도 매우 중요한 여러 성질들을 가지지만, 여기서는 Unitary의 경움나 다룬다. 이 존재성은 암호학 및 최근 계산복잡도적 제약에서 정보이론을 새롭게 해석하려는 시도인 Modern Quantum Information Theory 및 Computational Resource Theory에 큰 영향을 미칠 것으로 기대한다.

## Notation

Notation을 먼저 정의해 보고자 한다. 참고로 매우매우 길며 무려 논문의 20페이지 가량을 차지한다. 최대한 사용할 Notation만 정리해서 전달해 보려고 한다.

$$
N := 2^{n}
$$

$$
[N] := \{1,...,N\}
$$

$$
 \forall 1 \leq t \leq N, \quad [N]^{t}_{\textrm{dist}}:=\{(x_{1}, ..., x_{t}) \in [N]^{t} | x_{i} \neq x_{j} \textrm \: {for \: all} \: i \neq j \}
$$

즉, 1~N 까지 범위에서 t개의 숫자를 뽑아 하나씩 써서 t-tuple을 구성한다는 뜻이다. 이때, 가능한 총 경우의 수는 $$ \binom {N} {t} \times t! = \frac {N!} {(N-t)!}$$ 이다. 또한, $$ t = 0 $$ 일 때,  $$ \quad [N]^{t}_{\textrm{dist}} = \{()\} $$ 이다.

$$
\begin{aligned}
S_{\pi} : &(\mathbb{C}^{N})^{t} \longrightarrow (\mathbb{C}^{N})^{t} \\
&\ket{x_{1}, ..., x_{t}} \longmapsto \ket{x_{\pi^{-1}(1)}, ..., x_{\pi^{-1}(t)}}
\end{aligned}
$$

<div class="definition-box">
<b>Definition 1. (Relation)</b><br>
ordered pair \( (x_{i}, y_{i}) \in [N]^2 \) 에 대해, relation  
\( R = \{ (x_1, y_1), (x_2, y_2), \dots, (x_t, y_t) \} \) 인 multiset으로 정의한다.<br>
\( \mathcal{R} \): 모든 relation \( R \)에 대한 infinite set (즉, 집합의 집합)<br>
\( \mathcal{R}_{t} \): \( t \geq 0 \)일 때, 모든 size-\( t \)의 relation \( R \)에 대한 set<br>
</div>

<div class="definition-box">
<b>Definition 2. (Domain, Image)</b> <br>
relation \( R \)에 대해, <br>
\( Dom(R) = \{ x|x \in [N], \: \exists y \: \textrm{s.t.} \: (x, y) \in R \}\)<br>
\( Im(R) = \{ y|y \in [N], \: \exists x \: \textrm{s.t.} \: (x, y) \in R \}\)<br>
</div>

즉, 각 $$(x, y)$$ 는 어떠한 mapping에 대해 input $$ x $$ 에 대한 output $$ y $$ 를 pair로 모아놓은 것이고 여러 pair를 모아 놓은 것을 Relation의 정의라고 이해할 수 있다.

<div class="definition-box">
<b>Notation 1. (Relation state)</b> <br>
relation \( R \)에 대해, <br>
relation state \( \ket{R} := \frac {\sum_{\pi \in \textrm{Sym}_{t}} \ket{x_{\pi(1)}, y_{\pi(1)}, ..., x_{\pi(t)}, y_{\pi(t)}}} {\sqrt{t! \sum_{(x,y) \in [N]^{2}} \textrm{num}(R(x,y))!}} \)<br>
이때, \( \textrm{num}( \cdot ) \) 은 \( R \) 에서 \( (x, y) \) 가 나타낸 개수
</div>