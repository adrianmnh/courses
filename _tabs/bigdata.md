---
title: Big Data Algorithms
icon: fa-solid fa-database
order: 7
math: true
---

# Probability Review

## Bernouli Distribution

Denotes an event that takes on 2 possible values, $success(p)$ or $failure(q)$

$P(X=1)=p  \ \ \ \ and\  \ \ \  P(X=0)=1-p=q$

$E(X)=p \ \ \ and\ \ \ Var(X)=pq$

## Binomial Distribution

Denotes the probability that a number of success or failed events take place(Bernoulis)

Satisfies:
1. Binary outcome(Bernouli)
2. Independent
3. $n \text{ \# of trials}$
4. Same probability of success or failure per trial

$P(X=k) = {n \choose k}p^kq^{n-k} \text{ where k}\in\{0,1,2,..,n\}$

$E(X)=np \ \ \ \ and\ \ \ Var(X)=npq$

## Geometric Distribution

Used to find the probability of getting $1^{st}$ success or failure on trial $X$

Using the same conditions as Binomial Distribution

$P(X=k) = q^{k-1}p$

$E(X)=1/p \ \ \ and\ \ \ Var(X)=q/p^2$

### `notes:`

* $lg(n) \rightarrow base\ 2$
* $log(n) \rightarrow base\ 10$
* $ln(n) \rightarrow base \ e$

* If $\large I_A=1\ when\ x\ge t, \ then\ Pr(I=1)=Pr(x\ge t)$
* $\text{Indicator Random Variable: ExpectedValue(}I_A \text{) is equal to prob of event A ocurring}$
  * $\large E(I_A) = P(A) = p$
* Variance and Deviation $\mu$
  * $\sqrt{Var(X)} = \mu$
  * $Var(X) = \mu^2$
  * $\large Var(X) = E[(X-E[X])^2]$
  * $\large Var(X) = E[X^2] - E[X]^2$

* Tail bounds
  * Markov's - $Pr(X \ge t)\leq \Large \frac{E(X)}{t}$
  * ChebyShev's -  $Pr(X \ge t) \le Pr(\|X - E(X) \|\ge t )\le\Large \frac{Var(X)}{t^2}$
 



<!----------------------------------------------------------------------------------------------------------------------------->
![](\linebreak-fire.png)


# Membership(Dictionary Problem)

We want to construct an **algo/data structure** that stores elements in $S$ to answer membership queries

`binary search trees(BSTs)`
* Includes AVL, Red-Black, Splay trees

$\phi\ BST$ | Cost
:-:|:-:
Space Cost     | $O(n\ elements \times log(n) \ bits) \approx O(n)$
Pre-Processing | $O(n)\rightarrow \text{ proportional to \# of added elements}$
Query Cost     | $lg(n)$

Can **querying cost** be reduced?

`Hash Functions/tables/maps/compression functions`

$h[u]\rightarrow[m]\text{ such that u is strictly larger than m } u \gg m$

$m$ is the number of buckets or slots available in array or table $T$, used to store hashed elements with $h$

Collitions arrise because $u \gg m$ so by Pigeon Hole Principle, at least 2 objects in $[u]$ map to at least 1 object in $[m]$

Hashing with chaining is used to handle collisions, pointers to linked lists on each bucket $m$ (usually inserted in the front to reduce cost) 

Query time is proportional to the length of linked list of bucket $m$ in which object $x$ maps to using hash function $h$
1. worst case: every element in $S$ maps to 1 bucket $[u]\rightarrow\ c$
2. best case: `simple hash function:` every element $i \in [u]$ is mapped uniformly at random, $h:[u]\rightarrow [m]$ 
   * $Pr(h(i)=j)=1/m$ 

$\phi\ hash$ | Cost
:-:|:-:
Space Cost     | $O(n)$
Pre-Processing | $O(n)$
Query Cost     | $O(n)\ ...\ O(1/m)$

## Simple **Uniform** Hash Function

`Query Time Analysis and Proof`

Let $Q$ be query time for hashing w/ chain struct $1\le Q\le n$

`theorem:` assuming $h$ is uniform, the **expected value or mean:**

$E(Q)=O(n/m)$

`proof:` query time for any item $x_i$ is **dependent** on the # of distinct elements $x_j(j\ne i)$ that hash to the same bucket $:[m]$

This counts the number of collisions by setting probability to 1 if any to different elements map to the same bucket $[m]$, 0 otherwise

Using Indicator r.v., the fact that $\text{Pr(of element hashing to some bucket)} = \LARGE \frac{1}{m}$ and that $E(I_A)=Pr(A)$

$$Q(x) = \begin{cases}
\ 1,\ h(x_i)=h(x_j), i \ne j
\\
\ 0,\ otherwise
\end{cases}$$

$$\text{query time } Q = \sum_{i=1}^n E(X_i)= E\left(\sum_{i=1}^n X_i\right) = E\left(\sum_{i=1}^n \frac{1}{m}\right) = \frac{n}{m}
\\ 
\text{in expectation, }
\\
 Q = \large O\left(\frac{n}{m}\right)$$

 `disclaimer:` how well a simple uniform hash performs depends on how close $m$ is to $S$. If $S \gg m$ then the linked lists will be too large to search 

 1. If $m=O(n)$, then $E(Q)=O(1)$
 2. Hashing w/ chaining provides $O(1)$ **expected Query Time** $\iff$ the # of elements in $S$ is proportional to the # of slots $[m]$
 3. often more items that slots available → `Not the best structure`
 4. $P(Q_X)$ = Probability that $h$ uniformly hashes to bucket $[m]$

 $\phi\ chaining$ | Cost
:-:|:-:
Space Cost     | $O(n)$
Pre-Processing | $O(n)$
Query Cost     | $O(1) \text{ iff proportional } S\ to\ [m]$
Query Time:    | $P(Q_X) = \Large \frac{1}{m}$
Expectation:   | $E(Q_X) = \Large\left(\frac{n}{m}\right)$




<!----------------------------------------------------------------------------------------------------------------------------->
![](\linebreak-fire.png)


# **Tail Bounds**

What is the probability our result will deviate from the expectation? aka `bad event` 

## **Markov's Inequality**

Let $X$ be a r.v. over sample space $\Omega$ then $\forall_t \in R, t>0$

* What is the probability the **actual value** is beyond **expected value** by a factor of $t$
$$\large Pr(X\ge t.E(X)) \leq \frac{1}{t} \\ \equiv \\ Pr(X \ge t)\leq \frac{E(X)}{t}$$

`disclaimer:` Markov's Inequality is often too weak to yield any useful results. 

1. Fundamental tool in developing more sophisticated bounds. 
   * Use tail bounds to control $[m]$(size of table) to get a $O(1)$ query time (in expectation).
2. Techniques for bounding tail distribution are the major tool for estimating 
   * $Prob(failure)$ of algorithms, and
   * $High\ probability\ bounds$ on their run-time

`proof:` for $t > 0$, let $I_A = \begin{cases}
\ 1,\ if X\ge t
\\
\ 0,\ o.w.
\end{cases}$  , note that $X\ge 0$ 

$\text{first: Prove that } \ I_A\le X/t$

We have two possible outcomes: 
1. $I_A = 1$ if the event $X\ge t$ occurs, and
2. $I_A = 0$ if $X < t$. note that $t>0$

$t.I_A \le X ⇒ t.1 \le X$ if event occurs  and $t.I_A \le X ⇒ t.0 \le X$ if event does not occur

1. $t\le X$ is **true**
2. $0\le X$ also **true**

therefore, $t.I_A \le X \ \ ⇒ \ \ \large I_A\le\frac{X}{t}$ 

$\text{second: } \ I_A=[0,1], E(I_A) = Pr(I_A=1) = Pr(X\ge t)$

Taking expectations:

$Pr(X\ge t) = E[I_A] \text{ by linearity of expectations}$ 

$E[I_A] \le E[X/t]$

$E[X/t] =  \frac{\large E[X]}{\large t}$

$\text{finally: } Pr(X\ge t) \le \frac{\large E[X]}{\large t}$



## **ChebyShev's Inequality**

Let $X$ be a r.v. over sample space $\Omega$ then $for \ \forall\ t >0$


$$\large Pr(\ \left|X-E(X)\right| \ge t\ )\le \frac{Var[X]}{t^2}$$


`disclaimer:` Significantly **stronger tailbound** using expectaion and variance of a r.v.

`proof:` 

$\text{first: } Pr(\|X-E(X)\| \ge t) = Pr([X-E(X)]^2 \ge t^2)$ 

Since $[X-E(X)]^2$ is a non-negative r.v., apply Markov's

$\text{second: } \ Pr([X-E(X)]^2 \ge t^2) = E([X-E(X)]^2)/t^2$

$\text{next: } \  E([X-E(X)]^2)/t^2 = Var(X)/ t^2$


$\large \text{finally: } \ Pr([X-E(X)]^2 \ge t^2) = Pr(\ \|X-E(X)\| \ge t\ ) = \frac{\large Var[X]}{\Large t^2}$



`Using Chebyshev to bound Query Time:`

$$\large P(\left|Q_x - E(Q_x)\right| > t) \le \frac{\large n(\LARGE \frac{1}{m})(\large 1-\LARGE \frac{1}{m})}{t^2}  \large < \frac{E(X)}{t}$$

$\large n(1/m)(1 - 1/m) = np(1-p) = npq$



<!----------------------------------------------------------------------------------------------------------------------------->
![](\linebreak-fire.png)


# **Universal Hash Function**

Let $U$ be a universe of keys and $H$ be a finite collection of hash functions $h:[u]⇒[m]$

$H$ is `universal` if













<!----------------------------------------------------------------------------------------------------------------------------->
![](\linebreak-fire.png)

## **Chernoff Bound**

Let $X_1, X_2, ..., X_n$ be a Bernouli R.V. set $Pr\{X_i=1\}=P_i$, and can be written as $\large X = \sum_{i=1}^n X_i$ and $\delta \in R$, then:

1. $\text{If } 0\le \delta < 1,\large Pr\{X > (1 +\delta)(E[X])\} \le \large{e}\Large^{\frac{1}{3}\delta^2E(X) } \normalsize = \Large \frac {\large 1}{\Large e^{\Large \frac{1}{3}\large\delta^2E(X)}}$ 
   * if $\large c$ `is large`, then  $\frac{1}{\large e^{\normalsize c}}$`is very small`

2. $\forall\ \delta > 0, \large Pr\{X\ge (1+\delta)(E[X])\}\le \large \left( \frac{\large e^{\normalsize \delta}}{\large (1+\delta)^{\normalsize 1+\delta}}  \right)^{\normalsize E(X)}$
   * $Pr\{x\ge (1+\delta)(E[X])\}$ `is a bad event`

`We want to know:` $Pr(Y\ge B):$

Define $X_i = \begin{cases} 1, \ if\ i^{th }\text{ key maps to the block } ⇒\ Y = \large \sum_{i=1}^n X_i  
\\ 0,\ ow\end{cases}$

Let $\delta=\Large\frac{1}{n}\normalsize-1, then$

$$\large Pr\{Y\ge B\}=Pr\{Y\ge (1+\left(\large\frac{1}{n}\normalsize- 1\right))E[Y]\}$$

$$\large \le \left( \frac{e^{\normalsize\delta}}{(1+\delta)^{\normalsize1+\delta}}\right)^{\normalsize E(X)} = 
\left( \frac{e^{\normalsize\left(\frac{1}{n}\normalsize-1\right)}}{(1+\Large\frac{1}{n}\normalsize-1)^{\normalsize1+\Large\frac{1}{n}\normalsize-1}}\right)^{\normalsize E(X)}$$




<!----------------------------------------------------------------------------------------------------------------------------->
![](\linebreak-fire.png)

# Streaming Model

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
    * $Pr(X_j \text{ is an element of the set } A_{k+1}\mid X_j\text{ is not in }A_k)=0$

3. `probability that some element is in the new and the previous one is EQUAL TO (1 - probability that element is in previous but not in the new set)`
   * $Pr(X_j \in A_{k+1} \mid X_j \in A_k) = 1 - Pr(X_j \notin A_{k+1} \mid X_j \in A_k)$`

4. `Pr(some element is in the new set) = Pr(element is in new set\|element is in previous set).Pr(element is in previous set) + Pr(element is in new set\|element is not in previous set).Pr(element is not in previous set)`
   * $Pr(A) = Pr(A\mid B) Pr(B) + Pr(A\mid B^c).Pr(B^c)$

So, $\text{Pr(element is new set|element is not in previous set) = 0}$

Then, $Pr(X_j \in A_{k+1} ) = Pr(X_j \in A_{k+1}\mid X_j \in A_k).Pr(X_j \in A_k) + 0*Pr(X_j \notin A_k)$


$Pr(X_j\in A_{k+1}\mid X_j \in A_k) = 1-Pr(X_j \notin A_{k+1}\mid X_j\in A_k)$

$\text{Pr(element is not in new set given that it is in the previous set)=Pr(element got booted in the current iteration }\times \text{which element got booted)} = S/(k+1) \times 1/S$

$Pr(X_j \in A_{k+1} \mid X_j \in A_k) = 1-S/(k+1) \times 1/S = k/(k+1)$

$\text{Finally, }Pr(X_j \in A_{k+1} ) = k/(k+1) \times S/k + 0 = \Large \frac{S}{k+1}$


<!----------------------------------------------------------------------------------------------------------------------------->
![](\linebreak-fire.png)

