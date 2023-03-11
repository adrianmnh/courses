---
title: Big Data Algorithms
icon: fa-solid fa-database
order: 7
math: true
---

# `Streaming Model`

Used when:

* limited space
* elements come one at a time
* elements seen once may never appear again
* results may be approximations

Space for the whole stream: $m$

Goal:

**$log(m) \ or \ polylog(m)$**

To represent a single number of magnitude n, we need log n bits.

`Number n -> log n bits`

## Sampling Problem

Given a stream and unknown integer S.

1. At every point `i`, maintain a set A of size S containing elements from the stream `uniformly`
2. Every element of the stream should have equal chance of being the the set

## Algorithm
$S$ - random integer

$A$ - set of size S

$X_j$ - randomly chosen from $A_{i-1}$ →  `any element from the current set with` $Prob=S/i$ 

1. Put first $S$ elements from stream in set $A$
2. Let $A_i$ be the sample at time i
    1. for $i>S:$ 
       1. swap $X_i$ with $X_j$ `current from stream with randomly chosen from set`

## Claim 

At every point $i$, $X_j$ is in the set $A_i$ with $Prob=S/i$ 

## Proof By Induction

`Base Case:` $i \leq S,\  Pr(X_j \text{ in } A_i)= 1$

`Assume algorithm is correct for all i up to K:` $\ \forall \ 1\leq i\leq k$

`By inductive hypothesis(IH):` This means $A_k=\{X_1, X_2, X_3, ... , X_k\}$ and every element is in this sample with $Pr = S/k$ 

`Using these facts: ` 

1. `given: Pr(A) ~ Pr(latest stream element will be placed in the set A)`
   * $Pr(X_{k+1} \text{ is an element of the set }A_{k+1})=S/K+1$

2. `probability that some element is in the new set, given that it wasn't in the previous iteration`
    * $Pr(X_j \text{ is an element of the set } A_{k+1} | X_j \text{ is not in }A_k)=0$

3. `probability that some element is in the new and the previous one is EQUAL TO (1 - probability that element is in previous but not in the new set)`
   * $Pr(X_j \isin A_{k+1} | X_j \isin A_k) = 1 - Pr(X_j \notin A_{k+1} | X_j \isin A_k)$`

4. `Pr(some element is in the new set) = Pr(element is in new set|element is in previous set).Pr(element is in previous set) + Pr(element is in new set|element is not in previous set).Pr(element is not in previous set)`
   * $Pr(A) = Pr(A|B) Pr(B) + Pr(A|B^c).Pr(B^c)$

So, $\text{Pr(element is new set|element is not in previous set) = 0}$

Then, $Pr(X_j \isin A_{k+1} ) = Pr(X_j \isin A_{k+1}|X_j \isin A_k).Pr(X_j \isin A_k) + 0*Pr(X_j \notin A_k)$


$Pr(X_j \isin A_{k+1} | X_j \isin A_k) = 1 - Pr(X_j \notin A_{k+1} | X_j \isin A_k)$

$\text{Pr(element is not in new set given that it is in the previous set)=Pr(element got booted in the current iteration }\times \text{which element got booted)} = S/(k+1) \times 1/S$

$Pr(X_j \isin A_{k+1} | X_j \isin A_k) = 1-S/(k+1) \times 1/S = k/(k+1)$

Finally, $Pr(X_j \isin A_{k+1} ) = k/(k+1) \times S/k + 0 = S/(k+1)$

