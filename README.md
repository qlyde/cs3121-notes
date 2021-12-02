# COMP3121

***[use light mode]***

## Table of Contents

0. [Course Outline](#course-outline)
    - [Assessment](#assessment)
1. [Introduction](#introduction)
    - [Proofs](#proofs)
    - [Stable Matching Problem](#stable-matching-problem)
        * [Gale-Shapley Algorithm](#gale-shapley-algorithm)
2. [Divide and Conquer](#divide-and-conquer)
    - [Landau Notation](#landau-notation)
    - [Counting Inversions](#counting-inversions)
    - [Recurrences](#recurrences)
3. [Integer Multiplication I](#integer-multiplication-i)
    - [Master Theorem](#master-theorem)
    - [Arithmetic Operations](#arithmetic-operations)
4. [Integer Multiplication II](#integer-multiplication-ii)
    - [Generalising Karatsuba's Algorithm](#generalising-karatsubas-algorithm)
5. [Fast Fourier Transform](#fast-fourier-transform)
    - [Complex Numbers](#complex-numbers)
    - [The Fast Fourier Transform](#the-fast-fourier-transform)
6. [The Greedy Method](#the-greedy-method)
    - [Single Source Shortest Paths I](#single-source-shortest-paths-i)
        * [Dijkstra's Shortest Paths Algorithm](#dijkstras-shortest-paths-algorithm)
    - [Minimum Spanning Trees](#minimum-spanning-trees)
        * [Kruskal's Algorithm](#kruskals-algorithm)
        * [Union-Find](#union-find)
7. [Dynamic Programming](#dynamic-programming)
    - [Single Source Shortest Paths II](#single-source-shortest-paths-ii)
        * [Bellman-Ford Algorithm](#bellman-ford-algorithm)
    - [All Pairs Shortest Paths](#all-pairs-shortest-paths)
        * [Floyd-Warshall Algorithm](#floyd-warshall-algorithm)
8. [Maximum Flow](#maximum-flow)
    - [Flow Networks](#flow-networks)
    - [Residual Flow Networks](#residual-flow-networks)
    - [Augmenting Paths](#augmenting-paths)
    - [Solving the Maximum Flow Problem](#solving-the-maximum-flow-problem)
        * [Ford-Fulkerson Algorithm](#ford-fulkerson-algorithm)
        * [Edmonds-Karp Algorithm](#edmonds-karp-algorithm)
    - [Applications of Network Flow](#applications-of-network-flow)
    - [Bipartite Graphs](#bipartite-graphs)
9. [String Matching](#string-matching)
    - [Hashing](#hashing)
        * [Rabin-Karp Algorithm](#rabin-karp-algorithm)
    - [Finite Automata](#finite-automata)
        * [Knuth-Morris-Pratt Algorithm](#knuth-morris-pratt-algorithm)
10. [Linear Programming](#linear-programming)
    - [Weak Duality Theorem](#weak-duality-theorem)
11. [Intractability](#intractability)
    - [Feasibility of Algorithms](#feasibility-of-algorithms)
    - [Polynomial Reductions](#polynomial-reductions)
    - [Optimisation Problems](#optimisation-problems)

***

## Course Outline

### Assessment

* 4 assignments (10% each)
* Final Exam (60%)

## Introduction

* An algorithm is a collection of precisely defined steps that are executable using certain specified mechanical methods.
* By "mechanical" we mean the methods that do not involve any creativity, intuition or even intelligence.
* We deal with **sequential** (not **parallel**) and **deterministic** (not **randomised**) algorithms.

### Proofs

* Sometimes it is not obvious that an algorithm:
    - Terminates,
    - Will not run in exponentially many steps (in the size of the input), and
    - Produces a desired solution.
* Mathematical proofs are needed for such circumstances.

### Stable Matching Problem

* Suppose there are <img src="https://render.githubusercontent.com/render/math?math=n"> hospitals and <img src="https://render.githubusercontent.com/render/math?math=n"> doctors. Every hospital submits a list of doctor preferences and every doctor submits a list of hospital preferences.
* A **stable matching algorithm** produces a set of <img src="https://render.githubusercontent.com/render/math?math=n"> pairs <img src="https://render.githubusercontent.com/render/math?math=(h, d)"> for a hospital <img src="https://render.githubusercontent.com/render/math?math=h"> and a doctor <img src="https://render.githubusercontent.com/render/math?math=d"> so that the following never happens:
    - For two pairs <img src="https://render.githubusercontent.com/render/math?math=p = (h, d)"> and <img src="https://render.githubusercontent.com/render/math?math=p' = (h', d')">,
        * Hospital <img src="https://render.githubusercontent.com/render/math?math=h"> prefers doctor <img src="https://render.githubusercontent.com/render/math?math=d'"> **and**
        * Doctor <img src="https://render.githubusercontent.com/render/math?math=d'"> prefers hospital <img src="https://render.githubusercontent.com/render/math?math=h">.
* A stable matching always exists, but this is not obvious.

#### Gale-Shapley Algorithm

<img src="images/gale-shapley.png" alt="gale-shapley" width="70%"/>

* Claims to prove:
    - The algorithm terminates after <img src="https://render.githubusercontent.com/render/math?math=\le n^2"> iterations of the loop.
    - The algorithm produces a matching.
    - The matching is stable.

## Divide and Conquer

### Landau Notation

#### Big-O Notation

* We say <img src="https://render.githubusercontent.com/render/math?math=f(n) = O(g(n))"> if there exists positive constants <img src="https://render.githubusercontent.com/render/math?math=C"> and <img src="https://render.githubusercontent.com/render/math?math=N"> such that <img src="https://render.githubusercontent.com/render/math?math=0 \le f(n) \le C g(n)"> for all <img src="https://render.githubusercontent.com/render/math?math=n \ge N">.
* <img src="https://render.githubusercontent.com/render/math?math=g(n)"> is said to be an **asymptotic upper bound** for <img src="https://render.githubusercontent.com/render/math?math=f(n)">.
* Useful to (over-)estimate the complexity of a particular algorithm.

#### Big-<img src="https://render.githubusercontent.com/render/math?math=\Omega"> Notation

* We say <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Omega(g(n))"> if there exists positive constants <img src="https://render.githubusercontent.com/render/math?math=C"> and <img src="https://render.githubusercontent.com/render/math?math=N"> such that <img src="https://render.githubusercontent.com/render/math?math=0 \le C g(n) \le f(n)"> for all <img src="https://render.githubusercontent.com/render/math?math=n \ge N">.
* <img src="https://render.githubusercontent.com/render/math?math=g(n)"> is said to be an **asymptotic lower bound** for <img src="https://render.githubusercontent.com/render/math?math=f(n)">.
* Useful to say that an algorithm runs in at least <img src="https://render.githubusercontent.com/render/math?math=\Omega(g(n))">.

#### Properties

* <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Omega(g(n))"> if and only if <img src="https://render.githubusercontent.com/render/math?math=g(n) = O(f(n))">.
* We say <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Theta(g(n))"> if <img src="https://render.githubusercontent.com/render/math?math=f(n) = O(g(n))"> and <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Omega(g(n))">. That is, <img src="https://render.githubusercontent.com/render/math?math=f(n)"> and <img src="https://render.githubusercontent.com/render/math?math=g(n)"> have the same asymptotic growth rate.
* **Sum property:**
    - If <img src="https://render.githubusercontent.com/render/math?math=f_1 = O(g_1)"> and <img src="https://render.githubusercontent.com/render/math?math=f_2 = O(g_2)">, then <img src="https://render.githubusercontent.com/render/math?math=f_1 %2B f_2 = O(g_1 %2B g_2)">.
* **Product property:**
    - If <img src="https://render.githubusercontent.com/render/math?math=f_1 = O(g_1)"> and <img src="https://render.githubusercontent.com/render/math?math=f_2 = O(g_2)">, then <img src="https://render.githubusercontent.com/render/math?math=f_1 \cdot f_2 = O(g_1 \cdot g_2)">.
    - If <img src="https://render.githubusercontent.com/render/math?math=f = O(g)"> and <img src="https://render.githubusercontent.com/render/math?math=\lambda"> is a constant, then <img src="https://render.githubusercontent.com/render/math?math=\lambda \cdot f = O(g)">.
* These properties also hold for <img src="https://render.githubusercontent.com/render/math?math=\Omega">, <img src="https://render.githubusercontent.com/render/math?math=\Theta">, <img src="https://render.githubusercontent.com/render/math?math=o">, or <img src="https://render.githubusercontent.com/render/math?math=\omega">.
* <img src="https://render.githubusercontent.com/render/math?math=\log_a{n} = \Theta(\log_b{n})">, that is, logarithms of any base are interchangeable in asymptotic notation. For this reason we typically write <img src="https://render.githubusercontent.com/render/math?math=\log{n}"> instead.

### Counting Inversions

* Suppose there are <img src="https://render.githubusercontent.com/render/math?math=m"> users ranking the same set of <img src="https://render.githubusercontent.com/render/math?math=n"> movies. We want to determine for any two users <img src="https://render.githubusercontent.com/render/math?math=A"> and <img src="https://render.githubusercontent.com/render/math?math=B"> how similar their tastes are.
* Enumerate the movies on <img src="https://render.githubusercontent.com/render/math?math=B">'s list. For movie <img src="https://render.githubusercontent.com/render/math?math=i"> on <img src="https://render.githubusercontent.com/render/math?math=B">'s list we denote the position of that movie on <img src="https://render.githubusercontent.com/render/math?math=A">'s list as <img src="https://render.githubusercontent.com/render/math?math=a(i)">.

![inversions](images/inversions.png)

* A good measure of the degree of similarity between users <img src="https://render.githubusercontent.com/render/math?math=A"> and <img src="https://render.githubusercontent.com/render/math?math=B"> is to count the number of **inversions**.
* Inversions are the total number of pairs of movies <img src="https://render.githubusercontent.com/render/math?math=i">, <img src="https://render.githubusercontent.com/render/math?math=j"> such that movie <img src="https://render.githubusercontent.com/render/math?math=i"> precedes movie <img src="https://render.githubusercontent.com/render/math?math=j"> on <img src="https://render.githubusercontent.com/render/math?math=B">'s list but movie <img src="https://render.githubusercontent.com/render/math?math=j"> is higher than movie <img src="https://render.githubusercontent.com/render/math?math=i"> on <img src="https://render.githubusercontent.com/render/math?math=A">'s list.
    - That is, <img src="https://render.githubusercontent.com/render/math?math=i < j"> but <img src="https://render.githubusercontent.com/render/math?math=a(i) > a(j)">.
    - For example, 4 and 7 form an inversion because <img src="https://render.githubusercontent.com/render/math?math=5 = a(7) < a(4) = 8">.
* The brute force approach is a quadratic time algorithm <img src="https://render.githubusercontent.com/render/math?math=T(n) = \Theta(n^2)">. A divide and conquer approach can achieve time <img src="https://render.githubusercontent.com/render/math?math=O(n\log{n})">.
* We do a modified **merge sort** algorithm where we count inversions at the merge step.

![inversion-counting](images/inversion-counting.png)

* Each time we reach an element of <img src="https://render.githubusercontent.com/render/math?math=A_{hi}">, each remaining element to be merged in <img src="https://render.githubusercontent.com/render/math?math=A_{lo}"> counts as an inversion. In this diagram, when we merge 6 there are 5 remaining elements in <img src="https://render.githubusercontent.com/render/math?math=A_{lo}"> so we add 5 inversions.
* We add this number of inversions (across <img src="https://render.githubusercontent.com/render/math?math=A_{lo}"> and <img src="https://render.githubusercontent.com/render/math?math=A_{hi}">) to the number of inversions within <img src="https://render.githubusercontent.com/render/math?math=A_{lo}"> and <img src="https://render.githubusercontent.com/render/math?math=A_{hi}"> themselves.

### Recurrences

* Recurrences arise in estimations of time complexity of divide and conquer algorithms.
* Counting inversions in an array <img src="https://render.githubusercontent.com/render/math?math=A"> of size <img src="https://render.githubusercontent.com/render/math?math=n"> requires recursing on each half of the array (<img src="https://render.githubusercontent.com/render/math?math=A_{lo}"> and <img src="https://render.githubusercontent.com/render/math?math=A_{hi}">) and counting inversions across the partition in linear time.
    - <img src="https://render.githubusercontent.com/render/math?math=T(n) = 2T(\frac{n}{2}) %2B cn">
* Suppose a divide and conquer algorithm reduces a problem of size <img src="https://render.githubusercontent.com/render/math?math=n"> to <img src="https://render.githubusercontent.com/render/math?math=a"> many problems of smaller size <img src="https://render.githubusercontent.com/render/math?math=n/b"> with overhead cost <img src="https://render.githubusercontent.com/render/math?math=f(n)"> to split up the problem and combine the solutions.
    - <img src="https://render.githubusercontent.com/render/math?math=T(n) = aT(\frac{n}{b}) %2B f(n)">
    - Depth of recursion <img src="https://render.githubusercontent.com/render/math?math=\log_b{n}">
* To estimate an algorithm's efficiency we do not need the exact solution of a recurrence. We only need the **growth rate** of the solution (asymptotic behaviour) and the approximate **sizes of the constants** involved. (**Master Theorem**)

## Integer Multiplication I

### Master Theorem

* <img src="https://render.githubusercontent.com/render/math?math=T(n) = aT(\frac{n}{b}) %2B f(n)">
* Define the **critical exponent** <img src="https://render.githubusercontent.com/render/math?math=c^* = \log_b{a}"> and the **critical polynomial** <img src="https://render.githubusercontent.com/render/math?math=n^{c^*}">.

#### Theorem

> 1. If <img src="https://render.githubusercontent.com/render/math?math=f(n) = O(n^{c^* - \epsilon})"> for some <img src="https://render.githubusercontent.com/render/math?math=\epsilon > 0">, then <img src="https://render.githubusercontent.com/render/math?math=T(n) = \Theta(n^{c^*})">.
> 2. If <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Theta(n^{c^*})">, then <img src="https://render.githubusercontent.com/render/math?math=T(n) = \Theta(n^{c^*}\log{n})">.
> 3. If <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Omega(n^{c^* %2B \epsilon})"> for some <img src="https://render.githubusercontent.com/render/math?math=\epsilon > 0">, **and** for some <img src="https://render.githubusercontent.com/render/math?math=c < 1"> and some <img src="https://render.githubusercontent.com/render/math?math=n_0">, <img src="https://render.githubusercontent.com/render/math?math=af(\frac{n}{b}) \leq cf(n)"> holds for all <img src="https://render.githubusercontent.com/render/math?math=n > n_0">, then <img src="https://render.githubusercontent.com/render/math?math=T(n) = \Theta(f(n))">.
> 4. If none of these conditions hold, the Master Theorem is not applicable.

* <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Omega(n^{c^* %2B \epsilon})"> is a consequence of <img src="https://render.githubusercontent.com/render/math?math=af(\frac{n}{b}) \leq cf(n)">.

#### Example

* Let <img src="https://render.githubusercontent.com/render/math?math=T(n) = 4T(\frac{n}{2}) %2B n">.
* The critical exponent is <img src="https://render.githubusercontent.com/render/math?math=c^* = \log_b{a} = \log_2{4} = 2"> so the critical polynomial is <img src="https://render.githubusercontent.com/render/math?math=n^2">.
* <img src="https://render.githubusercontent.com/render/math?math=f(n) = n = O(n^{2 - \epsilon})"> for small <img src="https://render.githubusercontent.com/render/math?math=\epsilon">. (**Case 1**)
* Therefore <img src="https://render.githubusercontent.com/render/math?math=T(n) = \Theta(n^2)">.

### Arithmetic Operations

#### Addition

```
  C C C C C    carry
    X X X X X  first integer
+   X X X X X  second integer
-------------
  X X X X X X  result
```

* Adding 3 bits can be done in constant time and so the entire algorithm runs in linear time <img src="https://render.githubusercontent.com/render/math?math=O(n)">.
* There is no asymptotically faster algorithm to add two <img src="https://render.githubusercontent.com/render/math?math=n">-bit numbers because we have to read every bit of the input.

#### Multiplication

```
        X X X X  first integer
      * X X X X  second integer
      ---------
        X X X X  O(n^2) intermediate operations:
      X X X X      O(n^2) elementary multiplications
    X X X X        O(n^2) elementary additions
  X X X X
---------------
X X X X X X X X  result of length 2n
```

* Assume two `X`'s can be multiplied in <img src="https://render.githubusercontent.com/render/math?math=O(1)"> time.
* The above procedure runs in time <img src="https://render.githubusercontent.com/render/math?math=O(n^2)">.
* It is not known whether we can multiply two <img src="https://render.githubusercontent.com/render/math?math=n">-bit numbers in linear time.
* We can use divide and conquer to achieve faster than quadratic time.

#### Applying Divide and Conquer to Multiplication of Large Integers

* Split the two input numbers <img src="https://render.githubusercontent.com/render/math?math=A"> and <img src="https://render.githubusercontent.com/render/math?math=B"> into halves:
    - <img src="https://render.githubusercontent.com/render/math?math=A_0, B_0"> - the least significant <img src="https://render.githubusercontent.com/render/math?math=n/2"> bits.
    - <img src="https://render.githubusercontent.com/render/math?math=A_1, B_1"> - the most significant <img src="https://render.githubusercontent.com/render/math?math=n/2"> bits.
* <img src="https://render.githubusercontent.com/render/math?math=A = A_1 2^{n/2} %2B A_0">
* <img src="https://render.githubusercontent.com/render/math?math=B = B_1 2^{n/2} %2B B_0">
* <img src="https://render.githubusercontent.com/render/math?math=AB = A_1 B_1 2^n %2B (A_1 B_0 %2B A_0 B_1) 2^{n/2} %2B A_0 B_0">
* The 4 products <img src="https://render.githubusercontent.com/render/math?math=A_1 B_1">, <img src="https://render.githubusercontent.com/render/math?math=A_1 B_0">, <img src="https://render.githubusercontent.com/render/math?math=A_0 B_1"> and <img src="https://render.githubusercontent.com/render/math?math=A_0 B_0"> can be calculated recursively in the same manner.
* Each multiplication of two <img src="https://render.githubusercontent.com/render/math?math=n"> digit numbers is replaced by four multiplications of <img src="https://render.githubusercontent.com/render/math?math=n/2"> digit numbers. With the linear overhead to shift and add: <img src="https://render.githubusercontent.com/render/math?math=T(n) = 4T(n/2) %2B cn">.
* The critical exponent <img src="https://render.githubusercontent.com/render/math?math=c^* = \log_2{4} = 2"> so the critical polynomial is <img src="https://render.githubusercontent.com/render/math?math=n^2">. Then, <img src="https://render.githubusercontent.com/render/math?math=f(n) = cn = O(n^{2 - \epsilon})">. (**Case 1**)
* Therefore <img src="https://render.githubusercontent.com/render/math?math=T(n) = \Theta(n^2)">. We gained nothing from divide and conquer.

#### The Karatsuba Trick

* In 1960, Anatoly Karatsuba found an algorithm (later called "divide and conquer") that multiplies two <img src="https://render.githubusercontent.com/render/math?math=n">-digit numbers in <img src="https://render.githubusercontent.com/render/math?math=\Theta(n^{\log_2{3}}) \approx \Theta(n^{1.58...})">.
* Previously we saw that <img src="https://render.githubusercontent.com/render/math?math=AB = A_1 B_1 2^n %2B (A_1 B_0 %2B A_0 B_1) 2^{n/2} %2B A_0 B_0">.
* But rearranging, <img src="https://render.githubusercontent.com/render/math?math=AB = A_1 B_1 2^n %2B ((A_1 %2B A_0)(B_1 %2B B_0) - A_1 B_1 - A_0 B_0) 2^{n/2} %2B A_0 B_0">.
    - We save one multiplication at each round of recursion.
* 3 products <img src="https://render.githubusercontent.com/render/math?math=A_1 B_1">, <img src="https://render.githubusercontent.com/render/math?math=A_0 B_0"> and <img src="https://render.githubusercontent.com/render/math?math=(A_1 %2B A_0)(B_1 %2B B_0)">.
* <img src="https://render.githubusercontent.com/render/math?math=T(n) = 3T(n/2) %2B cn \implies T(n) = \Theta(n^{\log_2{3}}) = o(n^2)">

## Integer Multiplication II

### Generalising Karatsuba's Algorithm

* We try dividing the numbers <img src="https://render.githubusercontent.com/render/math?math=A">, <img src="https://render.githubusercontent.com/render/math?math=B"> into 3 pieces. With <img src="https://render.githubusercontent.com/render/math?math=k = n/3">,
    - <img src="https://render.githubusercontent.com/render/math?math=A = A_2 2^{2k} %2B A_1 2^k %2B A_0">, and
    - <img src="https://render.githubusercontent.com/render/math?math=B = B_2 2^{2k} %2B B_1 2^k %2B B_0">.
* The product <img src="https://render.githubusercontent.com/render/math?math=AB"> yields 5 coefficients and 9 products:
    - <img src="https://render.githubusercontent.com/render/math?math=AB = A_2 B_2 2^{4k} %2B (A_2 B_1 %2B A_1 B_2) 2^{3k} %2B (A_2 B_0 %2B A_1 B_1 %2B A_0 B_2) 2^{2k} %2B (A_1 B_0 %2B A_0 B_1) 2^k %2B A_0 B_0">
    - <img src="https://render.githubusercontent.com/render/math?math=C_4 = A_2 B_2">
    - <img src="https://render.githubusercontent.com/render/math?math=C_3 = A_2 B_1 %2B A_1 B_2">
    - <img src="https://render.githubusercontent.com/render/math?math=C_2 = A_2 B_0 %2B A_1 B_1 %2B A_0 B_2">
    - <img src="https://render.githubusercontent.com/render/math?math=C_1 = A_1 B_0 %2B A_0 B_1">
    - <img src="https://render.githubusercontent.com/render/math?math=C_0 = A_0 B_0">
    - These coefficients resemble **multiplying polynomials**.
* Write <img src="https://render.githubusercontent.com/render/math?math=P_A(x) = A_2 x^2 %2B A_1 x %2B A_0"> and <img src="https://render.githubusercontent.com/render/math?math=P_B(x) = B_2 x^2 %2B B_1 x %2B B_0"> where <img src="https://render.githubusercontent.com/render/math?math=A = P_A(2^k)"> and <img src="https://render.githubusercontent.com/render/math?math=B = P_B(2^k)">. We seek the coefficients of <img src="https://render.githubusercontent.com/render/math?math=P_C(x) = P_A(x) P_B(x)">.
* Let <img src="https://render.githubusercontent.com/render/math?math=P_C(x) = C_4 x^4 %2B C_3 x^3 %2B C_2 x^2 %2B C_1 x %2B C_0">.
* Since <img src="https://render.githubusercontent.com/render/math?math=P_C(x)"> is of degree 4, we need 5 values to **uniquely determine** it. For simplicity, we choose <img src="https://render.githubusercontent.com/render/math?math=-2, -1, 0, 1, 2">.
* We reconstruct <img src="https://render.githubusercontent.com/render/math?math=P_C(x)"> by evaluating <img src="https://render.githubusercontent.com/render/math?math=P_C(-2) = P_A(-2) P_B(-2)"> and <img src="https://render.githubusercontent.com/render/math?math=P_C(-1)">, <img src="https://render.githubusercontent.com/render/math?math=P_C(0)">, <img src="https://render.githubusercontent.com/render/math?math=P_C(1)">, <img src="https://render.githubusercontent.com/render/math?math=P_C(2)"> in a similar way.
* For <img src="https://render.githubusercontent.com/render/math?math=P_A(x) = A_2x^2 %2B A_1x %2B A_0"> we have,
    - <img src="https://render.githubusercontent.com/render/math?math=P_A(-2) = 4A_2 - 2A_1 %2B A_0">
    - <img src="https://render.githubusercontent.com/render/math?math=P_A(-1) = A_2 - A_1 %2B A_0">
    - <img src="https://render.githubusercontent.com/render/math?math=P_A(0) = A_0">
    - <img src="https://render.githubusercontent.com/render/math?math=P_A(1) = A_2 %2B A_1 %2B A_0">
    - <img src="https://render.githubusercontent.com/render/math?math=P_A(2) = 4A_2 %2B 2A_1 %2B A_0">
    - These only involve a constant number of additions (linear time).
* We require only 5 multiplications of large <img src="https://render.githubusercontent.com/render/math?math=n/3">-bit numbers:
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(-2) = P_A(-2)P_B(-2)">
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(-1) = P_A(-1)P_B(-1)">
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(0) = P_A(0)P_B(0)">
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(1) = P_A(1)P_B(1)">
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(2) = P_A(2)P_B(2)">
* To go from these 5 values to the coefficients that we seek, we solve a system of 5 linear equations in 5 variables:
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(-2) = C_4(-2)^4 %2B C_3(-2)^3 %2B C_2(-2)^2 %2B C_1(-2) %2B C_0">
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(-1) = C_4(-1)^4 %2B C_3(-1)^3 %2B C_2(-1)^2 %2B C_1(-1) %2B C_0">
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(0) = C_4(0)^4 %2B C_3(0)^3 %2B C_2(0)^2 %2B C_1(0) %2B C_0">
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(1) = C_4(1)^4 %2B C_3(1)^3 %2B C_2(1)^2 %2B C_1(1) %2B C_0">
    - <img src="https://render.githubusercontent.com/render/math?math=P_C(2) = C_4(2)^4 %2B C_3(2)^3 %2B C_2(2)^2 %2B C_1(2) %2B C_0">
* Using Gaussian elimination,
    * <img src="https://render.githubusercontent.com/render/math?math=C_0 = P_C(0)">
    * <img src="https://render.githubusercontent.com/render/math?math=C_1 = \frac{1}{12}[P_C(-2) - 8P_C(-1) %2B 8P_C(1) - P_C(2)]">
    * <img src="https://render.githubusercontent.com/render/math?math=C_2 = \frac{1}{24}[-P_C(-2) %2B 16P_C(-1) - 30P_C(0) %2B 16P_C(1) - P_C(2)]">
    * <img src="https://render.githubusercontent.com/render/math?math=C_3 = \frac{1}{12}[-P_C(-2) %2B 2P_C(-1) - 2P_C(1) %2B P_C(2)]">
    * <img src="https://render.githubusercontent.com/render/math?math=C_4 = \frac{1}{24}[P_C(-2) - 4P_C(-1) %2B 6P_C(0) - 4P_C(1) %2B P_C(2)]">
    * These expressions do not involve any multiplications of two large numbers and thus can be done in linear <img src="https://render.githubusercontent.com/render/math?math=O(n)"> time, where <img src="https://render.githubusercontent.com/render/math?math=n"> is the number of bits.
* With these coefficients, we can form the polynomial <img src="https://render.githubusercontent.com/render/math?math=P_C(x)"> and then compute <img src="https://render.githubusercontent.com/render/math?math=P_C(2^k)"> in linear time using bitwise shifts of the coefficients and a constant number of additions.
* Thus, we obtain <img src="https://render.githubusercontent.com/render/math?math=AB"> with only **5 multiplications**.
* Instead of multiplying two <img src="https://render.githubusercontent.com/render/math?math=n">-bit numbers, we do 5 multiplications of <img src="https://render.githubusercontent.com/render/math?math=n/3">-bit numbers with an overhead of additions, shifts, etc. all in linear time <img src="https://render.githubusercontent.com/render/math?math=cn">, so: <img src="https://render.githubusercontent.com/render/math?math=T(n) = 5T(n/3) %2B cn"> which by the Master Theorem gives <img src="https://render.githubusercontent.com/render/math?math=T(n) = \Theta(n^{\log_3{5}}) = O(n^{1.47})">.
* The original Karatsuba algorithm runs in <img src="https://render.githubusercontent.com/render/math?math=n^{1.58}"> and so we got a significantly faster algorithm.

#### The General Case I

* We generalise this and slice <img src="https://render.githubusercontent.com/render/math?math=A"> and <img src="https://render.githubusercontent.com/render/math?math=B"> into <img src="https://render.githubusercontent.com/render/math?math=p %2B 1"> many slices of <img src="https://render.githubusercontent.com/render/math?math=k"> bits. That is, <img src="https://render.githubusercontent.com/render/math?math=A"> and <img src="https://render.githubusercontent.com/render/math?math=B"> have <img src="https://render.githubusercontent.com/render/math?math=n = (p %2B 1)k"> bits.
* <img src="https://render.githubusercontent.com/render/math?math=A = A_p2^{pk} %2B A_{p-1}2^{(p-1)k} %2B \ldots %2B A_1 2^k %2B A_0">
* <img src="https://render.githubusercontent.com/render/math?math=B = B_p2^{pk} %2B B_{p-1}2^{(p-1)k} %2B \ldots %2B B_1 2^k %2B B_0">
* Then, <img src="https://render.githubusercontent.com/render/math?math=AB = \sum_{t=0}^{2p}\left(\sum_{i%2Bj=t}A_iB_j\right)2^{tk} = \sum_{t=0}^{2p}C_t2^{tk}">.
* As before, we form the polynomials <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> and <img src="https://render.githubusercontent.com/render/math?math=P_B(x)"> and let <img src="https://render.githubusercontent.com/render/math?math=P_C(x) = P_A(x)P_B(x)">.
* <img src="https://render.githubusercontent.com/render/math?math=P_C(x)"> is of degree <img src="https://render.githubusercontent.com/render/math?math=2p"> so we can evaluate <img src="https://render.githubusercontent.com/render/math?math=P_C(x_0) = P_A(x_0)P_B(x_0)"> at <img src="https://render.githubusercontent.com/render/math?math=2p %2B 1"> points, say <img src="https://render.githubusercontent.com/render/math?math=-p, \ldots, p">, and then reconstruct the polynomial from these values.

#### Convolution

* Define vectors <img src="https://render.githubusercontent.com/render/math?math=\vec{v} = (v_0, \ldots, v_r)"> and <img src="https://render.githubusercontent.com/render/math?math=\vec{w} = (w_0, \ldots, w_s)">. Then let <img src="https://render.githubusercontent.com/render/math?math=\vec{u} = (u_0, \ldots, u_{r%2Bs})"> such that <img src="https://render.githubusercontent.com/render/math?math=u_t = \sum_{i%2Bj=t}v_iw_j">. <img src="https://render.githubusercontent.com/render/math?math=\vec{u}"> is said to be the **linear convolution** of <img src="https://render.githubusercontent.com/render/math?math=\vec{v}"> and <img src="https://render.githubusercontent.com/render/math?math=\vec{w}">, denoted <img src="https://render.githubusercontent.com/render/math?math=\vec{u} = \vec{v} \star \vec{w}">.
* If we form polynomials with coefficients from <img src="https://render.githubusercontent.com/render/math?math=\vec{v}"> and <img src="https://render.githubusercontent.com/render/math?math=\vec{w}">, their product has coefficients given by <img src="https://render.githubusercontent.com/render/math?math=\vec{u}">.

#### The General Case II

* Evaluating <img src="https://render.githubusercontent.com/render/math?math=P_A(x_0)"> takes linear time <img src="https://render.githubusercontent.com/render/math?math=\Theta(k)"> since it requires <img src="https://render.githubusercontent.com/render/math?math=O(p^2)"> multiplications of a <img src="https://render.githubusercontent.com/render/math?math=k">-bit number <img src="https://render.githubusercontent.com/render/math?math=A_i"> by a constant.
* We then multiply large numbers <img src="https://render.githubusercontent.com/render/math?math=2p%2B1"> times <img src="https://render.githubusercontent.com/render/math?math=P_C(x_0) = P_A(x_0)P_B(x_0)">.
* We reconstruct these <img src="https://render.githubusercontent.com/render/math?math=2p %2B 1"> values of <img src="https://render.githubusercontent.com/render/math?math=P_C(x)"> to get the coefficients of the polynomial which requires <img src="https://render.githubusercontent.com/render/math?math=O(p^2)"> multiplications of a constant by a large number, which is linear time.
* At the multiplication step, <img src="https://render.githubusercontent.com/render/math?math=P_A(x) = A_px^p %2B A_{p-1}x^{p-1} %2B \ldots %2B A_0">.
    - Each <img src="https://render.githubusercontent.com/render/math?math=A_i"> is a <img src="https://render.githubusercontent.com/render/math?math=k">-bit number.
    - Each term <img src="https://render.githubusercontent.com/render/math?math=x^i"> has absolute value at most <img src="https://render.githubusercontent.com/render/math?math=p^p">.
    - There are <img src="https://render.githubusercontent.com/render/math?math=p %2B 1"> such terms.
* Therefore, <img src="https://render.githubusercontent.com/render/math?math=|P_A(x)| < (p%2B1)p^p2^k"> and so <img src="https://render.githubusercontent.com/render/math?math=\log_2|P_A(x)| < \log_2((p%2B1)p^p) %2B k">. Letting <img src="https://render.githubusercontent.com/render/math?math=s = \lfloor \log_2((p%2B1)p^p) \rfloor">, we see that the function values are <img src="https://render.githubusercontent.com/render/math?math=(k%2Bs)">-bit numbers, where <img src="https://render.githubusercontent.com/render/math?math=s"> is a constant.
* We have reduced a multiplication of two <img src="https://render.githubusercontent.com/render/math?math=n">-digit numbers to <img src="https://render.githubusercontent.com/render/math?math=2p %2B 1"> multiplications of <img src="https://render.githubusercontent.com/render/math?math=(k %2B s)">-digit numbers plus a linear overhead of additions, splitting, etc, so: <img src="https://render.githubusercontent.com/render/math?math=T(n) = (2p %2B 1)T\left(\frac{n}{p%2B1} %2B s\right) %2B \Theta(n)">.
* We ignore the constant <img src="https://render.githubusercontent.com/render/math?math=s"> and apply the Master Theorem to get <img src="https://render.githubusercontent.com/render/math?math=T(n) = \Theta(n^{\log_{p%2B1}(2p%2B1)})">.
* Note that <img src="https://render.githubusercontent.com/render/math?math=\log_{p%2B1}(2p%2B1) < \log_{p%2B1}2(p%2B1) = 1 %2B 1/\log_2(p%2B1)"> which can be made arbitrarily close to 1 by choosing a sufficiently large <img src="https://render.githubusercontent.com/render/math?math=p">.
* Therefore using a large enough number of slices allows us to get a runtime arbitarily **close to linear time**.
* However, for large <img src="https://render.githubusercontent.com/render/math?math=p">, evaluating <img src="https://render.githubusercontent.com/render/math?math=P_A(p) = A_pp^p %2B \ldots %2B A_0"> involves an **extremely large constant factor** <img src="https://render.githubusercontent.com/render/math?math=p^p">, resulting in a slow algorithm despite the fact that asymptotic bounds improve as <img src="https://render.githubusercontent.com/render/math?math=p"> increases.
* For this reason, Python implements multiplication of large numbers only using two slices (the original Karatsuba algorithm).

## Fast Fourier Transform

#### Context

* In our strategy to multiply polynomials fast, we:
    - Evaluated <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> and <img src="https://render.githubusercontent.com/render/math?math=P_B(x)"> at <img src="https://render.githubusercontent.com/render/math?math=2n %2B 1"> distinct points <img src="https://render.githubusercontent.com/render/math?math=x_0, \ldots, x_{2n}">,
    - Multiplied them point by point using <img src="https://render.githubusercontent.com/render/math?math=2n %2B 1"> multiplications of large numbers to get <img src="https://render.githubusercontent.com/render/math?math=2n %2B 1"> values of <img src="https://render.githubusercontent.com/render/math?math=P_C(x)">, and
    - Reconstructed the coefficients of <img src="https://render.githubusercontent.com/render/math?math=P_C(x) = C_{2n}x^{2n} %2B \ldots %2B C_1 x %2B C_0">.
* Previously we chose <img src="https://render.githubusercontent.com/render/math?math=x_0, \ldots, x_{2n}"> to be the <img src="https://render.githubusercontent.com/render/math?math=2n %2B 1"> integers <img src="https://render.githubusercontent.com/render/math?math=-n, \ldots, n"> which required us to compute values such as <img src="https://render.githubusercontent.com/render/math?math=P_A(n) = A_0 %2B A_1 n %2B \ldots %2B A_n n^n">. As the value of <img src="https://render.githubusercontent.com/render/math?math=n"> increases, the value of <img src="https://render.githubusercontent.com/render/math?math=n^n"> explodes causing a rapid increase in the computational complexity of our polynomial multiplication algorithm.
* We want to choose values for <img src="https://render.githubusercontent.com/render/math?math=x_0, \ldots, x_{2n}"> to avoid the explosion of size when we evaluate <img src="https://render.githubusercontent.com/render/math?math=x_i^n"> while computing <img src="https://render.githubusercontent.com/render/math?math=P_A(x_i)">. We would like <img src="https://render.githubusercontent.com/render/math?math=|x_i^n| = 1"> but this cannot be achieved with real numbers.

### Complex Numbers

* To multiply complex numbers, we multiply the moduli and add the arguments.

> If <img src="https://render.githubusercontent.com/render/math?math=z = re^{i\theta}"> and <img src="https://render.githubusercontent.com/render/math?math=w = se^{i\phi}">, then <img src="https://render.githubusercontent.com/render/math?math=zw = (rs)e^{i(\theta %2B \phi)}">.
>
> **Corollary.**
> If <img src="https://render.githubusercontent.com/render/math?math=z = re^{i\theta}">, then <img src="https://render.githubusercontent.com/render/math?math=z^n = r^{n}e^{i(n\theta)}">.

#### Complex Roots of Unity

* We are interested in the solutions of <img src="https://render.githubusercontent.com/render/math?math=z^m = 1">, known as **roots of unity of order** <img src="https://render.githubusercontent.com/render/math?math=m">.
* Solving <img src="https://render.githubusercontent.com/render/math?math=r^{m}e^{i(m\theta)} = 1">, we see that <img src="https://render.githubusercontent.com/render/math?math=r^m = 1 \Rightarrow r = 1"> and <img src="https://render.githubusercontent.com/render/math?math=m\theta = 2\pi k \Rightarrow \theta = 2\pi k/m">.
* Let <img src="https://render.githubusercontent.com/render/math?math=\omega_m = e^{i2\pi /m}">. Then <img src="https://render.githubusercontent.com/render/math?math=z = \omega_m^k">, i.e. all roots of unity of order <img src="https://render.githubusercontent.com/render/math?math=m"> can be written as powers of <img src="https://render.githubusercontent.com/render/math?math=\omega_m">. We say that <img src="https://render.githubusercontent.com/render/math?math=\omega_m"> is a **primitive root of unity of order** <img src="https://render.githubusercontent.com/render/math?math=m">. Note that there are only <img src="https://render.githubusercontent.com/render/math?math=m"> distinct values here, as <img src="https://render.githubusercontent.com/render/math?math=\omega_m^m = \omega_m^0">.

> <img src="https://render.githubusercontent.com/render/math?math=\omega_m^k"> is a primitive root of unity of order <img src="https://render.githubusercontent.com/render/math?math=m"> if and only if <img src="https://render.githubusercontent.com/render/math?math=\gcd(m,k) = 1">.

* The product of two roots of unity of order <img src="https://render.githubusercontent.com/render/math?math=m"> is given by <img src="https://render.githubusercontent.com/render/math?math=\omega_m^i \omega_m^j = \omega_m^{i %2B j}"> which is itself a root of unity of the same order.
* The set of all roots of unity of order <img src="https://render.githubusercontent.com/render/math?math=m">, <img src="https://render.githubusercontent.com/render/math?math=\{1, \omega_m, \omega_m^2, \ldots, \omega_m^{m-1}\}"> is closed under multiplication (and by extension, under taking powers).

> **Cancellation Lemma.**
> For all positive integers <img src="https://render.githubusercontent.com/render/math?math=l">, <img src="https://render.githubusercontent.com/render/math?math=m"> and integers <img src="https://render.githubusercontent.com/render/math?math=k">, <img src="https://render.githubusercontent.com/render/math?math=\omega_{lm}^{lk} = \omega_m^k">.

### The Fast Fourier Transform

* Given 2 polynomials of degree at most <img src="https://render.githubusercontent.com/render/math?math=n">, <img src="https://render.githubusercontent.com/render/math?math=P_A(x) = A_n x^n %2B \ldots %2B A_0"> and <img src="https://render.githubusercontent.com/render/math?math=P_B(x) = B_n x^n %2B \ldots %2B B_0"> we evaluate <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> and <img src="https://render.githubusercontent.com/render/math?math=P_B(x)"> at <img src="https://render.githubusercontent.com/render/math?math=m = 2n %2B 1"> distinct points <img src="https://render.githubusercontent.com/render/math?math=\omega_m^0, \omega_m^1, \ldots, \omega_m^{m-1}">.

#### The Discrete Fourier Transform (DFT)

> * Let <img src="https://render.githubusercontent.com/render/math?math=A = \langle A_0, A_1, \ldots, A_{m-1} \rangle"> be a sequence of <img src="https://render.githubusercontent.com/render/math?math=m"> real or complex numbers, and let the corresponding polynomial be <img src="https://render.githubusercontent.com/render/math?math=P_A(x) = \sum_{j=0}^{m-1}A_j x^j">.
> * Let <img src="https://render.githubusercontent.com/render/math?math=\hat{A}_k = P_A(\omega_m^k)"> for all <img src="https://render.githubusercontent.com/render/math?math=0 \leq k \leq m - 1">, the values of <img src="https://render.githubusercontent.com/render/math?math=P_A"> at the roots of unity of order <img src="https://render.githubusercontent.com/render/math?math=m">.
> * The sequence of values <img src="https://render.githubusercontent.com/render/math?math=\hat{A} = \langle \hat{A}_0, \ldots, \hat{A}_{m-1} \rangle"> is called the **Discrete Fourier Transform (DFT)** of <img src="https://render.githubusercontent.com/render/math?math=A">.

* Our polynomials <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> and <img src="https://render.githubusercontent.com/render/math?math=P_B(x)"> have degree <img src="https://render.githubusercontent.com/render/math?math=n">, so the corresponding sequences of coefficients have only <img src="https://render.githubusercontent.com/render/math?math=n %2B 1"> terms.
* We defined the DFT of a sequence as having the same length as the original sequence and we must obtain the values at all <img src="https://render.githubusercontent.com/render/math?math=m"> roots of unity of order <img src="https://render.githubusercontent.com/render/math?math=m">.
* We do this by padding the sequences <img src="https://render.githubusercontent.com/render/math?math=A"> and <img src="https://render.githubusercontent.com/render/math?math=B"> with zeroes corresponding to the terms <img src="https://render.githubusercontent.com/render/math?math=0x^{n%2B1} %2B \ldots %2B 0x^{2n}"> since <img src="https://render.githubusercontent.com/render/math?math=m = 2n %2B 1">.
* The DFT <img src="https://render.githubusercontent.com/render/math?math=\hat{A}"> of a sequence <img src="https://render.githubusercontent.com/render/math?math=A"> can be computed *very fast* using a divide and conquer algorithm called the **Fast Fourier Transform**.

#### The Fast Fourier Transform (FFT)

* We can now compute the DFTs of the two 0-padded sequences:
    - <img src="https://render.githubusercontent.com/render/math?math=DFT(\langle A_0, \ldots, A_n, \underbrace{0, \ldots, 0}_{n} \rangle) = \langle \hat{A}_0, \hat{A}_1, \ldots, \hat{A}_{m-1} \rangle">
    - <img src="https://render.githubusercontent.com/render/math?math=DFT(\langle B_0, \ldots, B_n, \underbrace{0, \ldots, 0}_{n} \rangle) = \langle \hat{B}_0, \hat{B}_1, \ldots, \hat{B}_{m-1} \rangle">
* For each <img src="https://render.githubusercontent.com/render/math?math=k"> we multiply the corresponding values <img src="https://render.githubusercontent.com/render/math?math=\hat{A}_k = P_A(\omega_m^k)"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{B}_k = P_B(\omega_m^k)">, obtaining <img src="https://render.githubusercontent.com/render/math?math=\hat{C}_k = \hat{A}_k \hat{B}_k = P_A(\omega_m^k)P_B(\omega_m^k) = P_C(\omega_m^k)">.
* We then use the **inverse transformation** for DFT, called **IDFT**, to recover the coefficients <img src="https://render.githubusercontent.com/render/math?math=\langle C_0, C_1, \ldots, C_{m-1} \rangle"> of the product polynomial <img src="https://render.githubusercontent.com/render/math?math=P_C(x)"> from the sequence <img src="https://render.githubusercontent.com/render/math?math=\langle \hat{C}_0, \ldots, \hat{C}_{m-1} \rangle">.
* We can assume that <img src="https://render.githubusercontent.com/render/math?math=m"> is a power of 2, otherwise we can pad <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> with zero coefficients until its number of coefficients becomes the nearest power of 2.

> For every <img src="https://render.githubusercontent.com/render/math?math=m"> which is not a power of 2, the smallest power of 2 larger or equal to <img src="https://render.githubusercontent.com/render/math?math=m"> is smaller than <img src="https://render.githubusercontent.com/render/math?math=2m">.

* **Problem.** Given a sequence <img src="https://render.githubusercontent.com/render/math?math=A = \langle A_0, \ldots, A_{m-1} \rangle">, compute its DFT, i.e. find the values <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> at <img src="https://render.githubusercontent.com/render/math?math=x = \omega_m^k"> for all <img src="https://render.githubusercontent.com/render/math?math=k"> such that <img src="https://render.githubusercontent.com/render/math?math=0 \leq k < m">.
* The idea is to use divide and conquer by splitting the polynomial <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> into the **even powers** and the **odd powers**:
    - <img src="https://render.githubusercontent.com/render/math?math=P_A(x) = A_0 %2B A_2 x^2 %2B A_4 (x^2)^2 %2B \ldots %2B A_{m-2} (x^2)^{m/2 - 1} %2B x(A_1 %2B A_3 x^2 %2B A_5 (x^2)^2 %2B \ldots %2B A_{m-1} (x^2)^{m/2 - 1})">
* Let us define <img src="https://render.githubusercontent.com/render/math?math=A^{[0]} = \langle A_0, A_2, \ldots, A_{m-2} \rangle"> and <img src="https://render.githubusercontent.com/render/math?math=A^{[1]} = \langle A_1, A_3, \ldots, A_{m-1} \rangle">. Note <img src="https://render.githubusercontent.com/render/math?math=m - 1"> is odd since we assume <img src="https://render.githubusercontent.com/render/math?math=m"> is a power of 2.
    - <img src="https://render.githubusercontent.com/render/math?math=P_{A^{[0]}}(y) = A_0 %2B A_2 y %2B A_4 y^2 %2B \ldots %2B A_{m-2} y^{m/2 - 1}">
    - <img src="https://render.githubusercontent.com/render/math?math=P_{A^{[1]}}(y) = A_1 %2B A_3 y %2B A_5 y^2 %2B \ldots %2B A_{m-1} y^{m/2 - 1}">
    - Hence, <img src="https://render.githubusercontent.com/render/math?math=P_A(x) = P_{A^{[0]}}(x^2) %2B xP_{A^{[1]}}(x^2)">.
    - The polynomials <img src="https://render.githubusercontent.com/render/math?math=P_{A^{[0]}}(y)"> and <img src="https://render.githubusercontent.com/render/math?math=P_{A^{[1]}}(y)"> each have <img src="https://render.githubusercontent.com/render/math?math=m/2"> coefficients while <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> has <img src="https://render.githubusercontent.com/render/math?math=m"> coefficients.
* We have reduced the problem from evaluating <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> with <img src="https://render.githubusercontent.com/render/math?math=m"> coefficients to evaluating two polynomials <img src="https://render.githubusercontent.com/render/math?math=P_{A^{[0]}}(y)"> and <img src="https://render.githubusercontent.com/render/math?math=P_{A^{[1]}}(y)"> each with <img src="https://render.githubusercontent.com/render/math?math=m/2"> coefficients at points <img src="https://render.githubusercontent.com/render/math?math=y = x^2 = \omega_m^{2k}">.
* Since <img src="https://render.githubusercontent.com/render/math?math=m"> is a power of 2, and hence even, we can use the cancellation lemma <img src="https://render.githubusercontent.com/render/math?math=y = \omega_m^{2k} = \omega_{m/2}^k"> to deduce that <img src="https://render.githubusercontent.com/render/math?math=y"> is a root of unity of order <img src="https://render.githubusercontent.com/render/math?math=m/2">.
    - Note <img src="https://render.githubusercontent.com/render/math?math=k"> goes up to <img src="https://render.githubusercontent.com/render/math?math=m - 1"> but there are only <img src="https://render.githubusercontent.com/render/math?math=m/2"> distinct roots of unity of order <img src="https://render.githubusercontent.com/render/math?math=m/2">. Thus we simplify the later terms as repetitions of the earlier terms.
* We can write <img src="https://render.githubusercontent.com/render/math?math=P_A(\omega_m^k) = P_{A^{[0]}}((\omega_m^k)^2) %2B \omega_m^k \cdot P_{A^{[1]}}((\omega_m^k)^2) = P_{A^{[0]}}(\omega_{m/2}^k) %2B \omega_m^k \cdot P_{A^{[1]}}(\omega_{m/2}^k)">.
    - We have reduced a problem of size <img src="https://render.githubusercontent.com/render/math?math=m"> to two such problems of size <img src="https://render.githubusercontent.com/render/math?math=m/2"> plus a linear overhead to multiply the <img src="https://render.githubusercontent.com/render/math?math=\omega_m^k"> terms.
* <img src="https://render.githubusercontent.com/render/math?math=T(m) = 2T(m/2) %2B cm"> which by **Case 2** of the Master Theorem gives <img src="https://render.githubusercontent.com/render/math?math=T(m) = \Theta(m\log{m}) = \Theta(n\log{n})"> since <img src="https://render.githubusercontent.com/render/math?math=m = 2n %2B 1">.
* FFT is a method of replacing <img src="https://render.githubusercontent.com/render/math?math=m^2"> many multiplications with a <img src="https://render.githubusercontent.com/render/math?math=\Theta(m\log{m})"> procedure.

#### The Inverse Fast Fourier Transform

* The evaluation of a polynomial <img src="https://render.githubusercontent.com/render/math?math=P_A(x) = A_0 %2B A_1 x %2B \ldots %2B A_{m-1}x^{m-1}"> at roots of unity <img src="https://render.githubusercontent.com/render/math?math=\omega_m^k"> of order <img src="https://render.githubusercontent.com/render/math?math=m"> can be represented by the matrix-vector product:
<img src="https://render.githubusercontent.com/render/math?math=\underbrace{\begin{pmatrix} 1 %26%26 1 %26%26 1 %26%26 \ldots %26%26 1 \\ 1 %26%26 \omega_m %26%26 \omega_m^2 %26%26 \ldots %26%26 \omega_m^{m-1} \\ 1 %26%26 \omega_m^2 %26%26 \omega_m^{2\cdot 2} %26%26 \ldots %26%26 \omega_m^{2(m-1)} \\ \vdots %26%26 \vdots %26%26 \vdots %26%26 \ddots %26%26 \vdots \\ 1 %26%26 \omega_m^{m-1} %26%26 \omega_m^{2(m-1)} %26%26 \ldots %26%26 \omega_m^{(m-1)(m-1)} \end{pmatrix}}_{M} \begin{pmatrix} A_0 \\ %0A A_1 \\ A_2 \\ \vdots \\ A_{m-1} \end{pmatrix} = \begin{pmatrix} P_A(1) \\ %0A P_A(\omega_m) \\ P_A(\omega_m^2) \\ \vdots \\ P_A(\omega_m^{m-1}) \end{pmatrix}">

* We need a way to reconstruct the coefficients from these values.
* Since <img src="https://render.githubusercontent.com/render/math?math=M"> is a square **Vandermonde matrix** with distinct rows, it is invertible, so:
<img src="https://render.githubusercontent.com/render/math?math=\begin{pmatrix} A_0 \\ A_1 \\ A_2 \\ \vdots \\ A_{m-1} \end{pmatrix} = M^{-1} \begin{pmatrix} P_A(1) \\ %0A P_A(\omega_m) \\ P_A(\omega_m^2) \\ \vdots \\ P_A(\omega_m^{m-1}) \end{pmatrix}">

> The inverse of matrix <img src="https://render.githubusercontent.com/render/math?math=M"> is found by simply changing the signs of the exponents and dividing by <img src="https://render.githubusercontent.com/render/math?math=m">.

* We get:
<img src="https://render.githubusercontent.com/render/math?math=\begin{pmatrix} A_0 \\ A_1 \\ A_2 \\ \vdots \\ A_{m-1} \end{pmatrix} = \frac{1}{m} \begin{pmatrix} 1 %26%26 1 %26%26 1 %26%26 \ldots %26%26 1 \\ %0A 1 %26%26 \omega_m^{-1} %26%26 \omega_m^{-2} %26%26 \ldots %26%26 \omega_m^{-(m-1)} \\ 1 %26%26 \omega_m^{-2} %26%26 \omega_m^{-2\cdot 2} %26%26 \ldots %26%26 \omega_m^{-2(m-1)} \\ \vdots %26%26 \vdots %26%26 \vdots %26%26 \ddots %26%26 \vdots \\ 1 %26%26 \omega_m^{-(m-1)} %26%26 \omega_m^{-2(m-1)} %26%26 \ldots %26%26 \omega_m^{-(m-1)(m-1)} \end{pmatrix} \begin{pmatrix} P_A(1) \\ %0A P_A(\omega_m) \\ P_A(\omega_m^2) \\ \vdots \\ P_A(\omega_m^{m-1}) \end{pmatrix}">

* This is not so different to the original matrix-vector product.
* The inverse FFT requires us to convert from the sequence of values <img src="https://render.githubusercontent.com/render/math?math=\langle P_A(1), P_A(\omega_m), P_A(\omega_m^2), \ldots, P_A(\omega_m^{m-1}) \rangle">, denoted by <img src="https://render.githubusercontent.com/render/math?math=\langle \hat{A}_0, \hat{A}_1, \ldots, \hat{A}_{m-1} \rangle"> back to the sequence of coefficients <img src="https://render.githubusercontent.com/render/math?math=\langle A_0, A_1, \ldots, A_{m-1} \rangle">.
* To do this we use the same FFT algorithm with 2 changes:
    - The root of unity <img src="https://render.githubusercontent.com/render/math?math=\omega_m"> is replaced by <img src="https://render.githubusercontent.com/render/math?math=\overline{\omega_m} = e^{-i(2\pi /m)}">, and
    - The resulting output values are divided by <img src="https://render.githubusercontent.com/render/math?math=m">.
* We can now compute the product <img src="https://render.githubusercontent.com/render/math?math=P_C(x) = P_A(x)P_B(x)"> of two polynomials <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> and <img src="https://render.githubusercontent.com/render/math?math=P_B(x)"> in time <img src="https://render.githubusercontent.com/render/math?math=\Theta(n\log{n})">.
    - Finding the DFTs <img src="https://render.githubusercontent.com/render/math?math=\hat{A}"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{B}"> of <img src="https://render.githubusercontent.com/render/math?math=P_A(x)"> and <img src="https://render.githubusercontent.com/render/math?math=P_B(x)"> each run in <img src="https://render.githubusercontent.com/render/math?math=\Theta(n\log{n})">.
    - Multiplying <img src="https://render.githubusercontent.com/render/math?math=\hat{A}"> and <img src="https://render.githubusercontent.com/render/math?math=\hat{B}"> to get <img src="https://render.githubusercontent.com/render/math?math=\hat{C}"> runs in <img src="https://render.githubusercontent.com/render/math?math=\Theta(n)">.
    - Finding the IDFT of <img src="https://render.githubusercontent.com/render/math?math=\hat{C}"> to get <img src="https://render.githubusercontent.com/render/math?math=P_C(x)"> runs in <img src="https://render.githubusercontent.com/render/math?math=\Theta(n\log{n})">.
    - Thus we can find the convolution of two <img src="https://render.githubusercontent.com/render/math?math=n">-term sequences in <img src="https://render.githubusercontent.com/render/math?math=\Theta(n\log{n})">.

## The Greedy Method

* A **greedy algorithm** is one that solves a problem by dividing it into stages, and rather than exhaustively searching all the ways to get from one stage to the next, instead only considers the choice that appears best. This obviously reduces the search space, but it is not always clear whether the locally optimal choice leads to the globally optimal outcome.
* The greedy method does not always work. Frameworks exist to determine whether a problem can be solved using a greedy algorithm.
* We focus on proving the correctness of greedy algorithms. There are two main methods of proof:
    - **Greedy stays ahead:** prove that at every stage, no other algorithm could do better than our proposed algorithm.
    - **Exchange argument:** consider an optimal solution, and gradually transform it to the solution found by our proposed algorithm without making it any worse.
* **See the example problems in [Lectures 6-8](resources/6-greedy.pdf).**
* [Proving Correctness of Greedy Algorithms](resources/proving-correctness-of-greedy-algorithms.pdf)

### Single Source Shortest Paths I

* Suppose we have a **directed graph** <img src="https://render.githubusercontent.com/render/math?math=G = (V, E)"> with *non-negative* weight <img src="https://render.githubusercontent.com/render/math?math=w(e) \geq 0"> assigned to each edge <img src="https://render.githubusercontent.com/render/math?math=e \in E"> and a designated (source) vertex <img src="https://render.githubusercontent.com/render/math?math=v \in V">.
* We want to find for every <img src="https://render.githubusercontent.com/render/math?math=u \in V"> the shortest path from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=u">.
* This is accomplished by a very elegant greedy algorithm developed by Edsger **Dijkstra** in 1959.

> For every vertex <img src="https://render.githubusercontent.com/render/math?math=w"> on a shortest path from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=z">, the shortest path from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w"> is just the truncation of that path ending at <img src="https://render.githubusercontent.com/render/math?math=w">.

#### Dijkstra's Shortest Paths Algorithm

* The algorithm builds a set <img src="https://render.githubusercontent.com/render/math?math=S"> of vertices for which the shortest path has already been established, starting with an empty set and adding one vertex at a time.
* At each stage of the construction, we add the vertex <img src="https://render.githubusercontent.com/render/math?math=u \in V \setminus S"> which has the shortest path from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=u"> with all intermediate vertices already in <img src="https://render.githubusercontent.com/render/math?math=S">.
    - The first vertex added to <img src="https://render.githubusercontent.com/render/math?math=S"> is <img src="https://render.githubusercontent.com/render/math?math=v"> itself, with path length zero.
* At each of <img src="https://render.githubusercontent.com/render/math?math=n"> steps, we scan an array of length <img src="https://render.githubusercontent.com/render/math?math=n">. We also run the constant time update procedure at most once for each edge. The algorithm therefore runs in <img src="https://render.githubusercontent.com/render/math?math=O(n^2 %2B m)">.
    - In a *simple graph* (no self loops or parallel edges) we have <img src="https://render.githubusercontent.com/render/math?math=m \leq n(n-1)"> so we can simplify this to <img src="https://render.githubusercontent.com/render/math?math=O(n^2)">.
* A more efficient implementation using an **augmented heap** can achieve a time complexity of <img src="https://render.githubusercontent.com/render/math?math=O((n%2Bm)\log{n})">. Assuming the graph is connected, <img src="https://render.githubusercontent.com/render/math?math=m \geq n - 1"> so we can simplify to <img src="https://render.githubusercontent.com/render/math?math=O(m\log{n})">.

### Minimum Spanning Trees

* A minimum spanning tree <img src="https://render.githubusercontent.com/render/math?math=T"> of a connected graph <img src="https://render.githubusercontent.com/render/math?math=G"> is a subgraph of <img src="https://render.githubusercontent.com/render/math?math=G"> (with the same set of vertices) which is a tree, and among all such trees it minimises the total length of all edges in <img src="https://render.githubusercontent.com/render/math?math=T">.
* Let <img src="https://render.githubusercontent.com/render/math?math=G"> be a connected graph with all lengths of edges <img src="https://render.githubusercontent.com/render/math?math=E"> of <img src="https://render.githubusercontent.com/render/math?math=G"> distinct and <img src="https://render.githubusercontent.com/render/math?math=S"> a non-empty proper subset of the set of all vertices <img src="https://render.githubusercontent.com/render/math?math=V"> of <img src="https://render.githubusercontent.com/render/math?math=G">. Assume that <img src="https://render.githubusercontent.com/render/math?math=e = (u, v)"> is an edge such that <img src="https://render.githubusercontent.com/render/math?math=u \in S"> and <img src="https://render.githubusercontent.com/render/math?math=v \notin S"> and is of minimal length among all the edges having this property. Then <img src="https://render.githubusercontent.com/render/math?math=e"> must belong to every minimum spanning tree <img src="https://render.githubusercontent.com/render/math?math=T"> of <img src="https://render.githubusercontent.com/render/math?math=G">.
* There are two famous greedy algorithms for the minimum spanning tree problem. Both algorithms build up a forest, beginning with all <img src="https://render.githubusercontent.com/render/math?math=n"> isolated vertices and adding edges one by one.
* **Prim's algorithm** uses one large component, adding one of the isolated vertices to it at each stage. This algorithm is very similar to Dijkstra's algorithm, but adds the vertex closest to <img src="https://render.githubusercontent.com/render/math?math=S"> rather than the one closest to the starting vertex <img src="https://render.githubusercontent.com/render/math?math=v">.

#### Kruskal's Algorithm

* We order the edges <img src="https://render.githubusercontent.com/render/math?math=E"> in a non-decreasing order of their weights.
* An edge <img src="https://render.githubusercontent.com/render/math?math=e"> is added if its inclusion does not introduce a *cycle* in the graph constructed thus far, or discarded otherwise.
* The process terminates when the forest is connected, i.e. when <img src="https://render.githubusercontent.com/render/math?math=n - 1"> edges have been added.
* Kruskal's algorithm produces a minimal spanning tree and if all weights are distinct then such a tree is unique.
* We need to quickly determine whether a certain new edge will introduce a cycle. An edge <img src="https://render.githubusercontent.com/render/math?math=e = (u, v)"> will introduce a cycle in the forest <img src="https://render.githubusercontent.com/render/math?math=F"> if and only if there is already a path between <img src="https://render.githubusercontent.com/render/math?math=u"> and <img src="https://render.githubusercontent.com/render/math?math=v">, i.e. <img src="https://render.githubusercontent.com/render/math?math=u"> and <img src="https://render.githubusercontent.com/render/math?math=v"> are in the same connected component.

#### Union-Find

* In our implementation of Kruskal's algorithm, we use a data structure called **Union-Find** which handles **disjoint sets**. This data structure supports three operations:
    - <img src="https://render.githubusercontent.com/render/math?math=\text{MakeUnionFind}(S)">, which returns a structure in which all elements are placed into distinct singleton sets. This operation runs in time <img src="https://render.githubusercontent.com/render/math?math=O(n)"> where <img src="https://render.githubusercontent.com/render/math?math=n = |S|">.
    - <img src="https://render.githubusercontent.com/render/math?math=\text{Find}(v)"> which returns the (label of the) set to which <img src="https://render.githubusercontent.com/render/math?math=v"> belongs. This operation runs in time <img src="https://render.githubusercontent.com/render/math?math=O(1)">.
    - <img src="https://render.githubusercontent.com/render/math?math=\text{Union}(A, B)"> which changes the data structure by replacing sets <img src="https://render.githubusercontent.com/render/math?math=A"> and <img src="https://render.githubusercontent.com/render/math?math=B"> with the set <img src="https://render.githubusercontent.com/render/math?math=A \cup B">. A sequence of <img src="https://render.githubusercontent.com/render/math?math=k"> initial consecutive <img src="https://render.githubusercontent.com/render/math?math=\text{Union}"> operations run in time <img src="https://render.githubusercontent.com/render/math?math=O(k\log{k})">.
* We do not give the runtime of a single <img src="https://render.githubusercontent.com/render/math?math=\text{Union}"> operation but a sequence of <img src="https://render.githubusercontent.com/render/math?math=k"> consecutive such operations. Such time complexity analysis is called **amortized analysis**; it estimates average cost of an operation in a sequence of operations, in this case <img src="https://render.githubusercontent.com/render/math?math=\log{k}">.
* <img src="https://render.githubusercontent.com/render/math?math=k"> *initial consecutive* <img src="https://render.githubusercontent.com/render/math?math=\text{Union}"> operations refers to the first <img src="https://render.githubusercontent.com/render/math?math=k"> <img src="https://render.githubusercontent.com/render/math?math=\text{Union}"> operations performed after <img src="https://render.githubusercontent.com/render/math?math=\text{MakeUnionFind}">. There may be <img src="https://render.githubusercontent.com/render/math?math=\text{Find}"> operations between these.
* <img src="https://render.githubusercontent.com/render/math?math=S"> is the vertex set <img src="https://render.githubusercontent.com/render/math?math=V"> of a graph, of the form <img src="https://render.githubusercontent.com/render/math?math=\{1, 2, \ldots, n\}">. We will label each set by one of its elements, called the *representative* of the set.
* The simplest implementation:
    - An array <img src="https://render.githubusercontent.com/render/math?math=A"> such that <img src="https://render.githubusercontent.com/render/math?math=A[i] = j"> means that <img src="https://render.githubusercontent.com/render/math?math=i"> belongs to the set with representative <img src="https://render.githubusercontent.com/render/math?math=j">,
    - An array <img src="https://render.githubusercontent.com/render/math?math=B"> such that <img src="https://render.githubusercontent.com/render/math?math=B[i]"> contains the number of elements in the set with representative <img src="https://render.githubusercontent.com/render/math?math=i">, and
    - An array <img src="https://render.githubusercontent.com/render/math?math=L"> such that <img src="https://render.githubusercontent.com/render/math?math=L[i]"> contains pointers to the head and tail of a linked list containing the elements of the set with representative <img src="https://render.githubusercontent.com/render/math?math=i">.
* If <img src="https://render.githubusercontent.com/render/math?math=i"> is not the representative of any set, then <img src="https://render.githubusercontent.com/render/math?math=B[i]"> is zero and the list <img src="https://render.githubusercontent.com/render/math?math=L[i]"> is empty.
* <img src="https://render.githubusercontent.com/render/math?math=\text{Union}(i, j)"> with two sets <img src="https://render.githubusercontent.com/render/math?math=I"> and <img src="https://render.githubusercontent.com/render/math?math=J"> with representatives <img src="https://render.githubusercontent.com/render/math?math=i"> and <img src="https://render.githubusercontent.com/render/math?math=j"> is defined as:
    - Assume <img src="https://render.githubusercontent.com/render/math?math=|I| \geq |J|"> (i.e. <img src="https://render.githubusercontent.com/render/math?math=B[i] \geq B[j]">) otherwise perform <img src="https://render.githubusercontent.com/render/math?math=\text{Union}(j, i)"> instead.
    - For each <img src="https://render.githubusercontent.com/render/math?math=m \in J">, update <img src="https://render.githubusercontent.com/render/math?math=A[m]"> from <img src="https://render.githubusercontent.com/render/math?math=j"> to <img src="https://render.githubusercontent.com/render/math?math=i">.
    - Update <img src="https://render.githubusercontent.com/render/math?math=B[i]"> to <img src="https://render.githubusercontent.com/render/math?math=B[i] %2B B[j]"> and <img src="https://render.githubusercontent.com/render/math?math=B[j]"> to zero.
    - Append the list <img src="https://render.githubusercontent.com/render/math?math=L[j]"> to the list <img src="https://render.githubusercontent.com/render/math?math=L[i]"> and replace <img src="https://render.githubusercontent.com/render/math?math=L[j]"> with an empty list.

#### Efficient Implementation of Kruskal's Algorithm

* We first sort the <img src="https://render.githubusercontent.com/render/math?math=m"> edges of graph <img src="https://render.githubusercontent.com/render/math?math=G"> which takes <img src="https://render.githubusercontent.com/render/math?math=O(m\log{m})">. Since <img src="https://render.githubusercontent.com/render/math?math=m < n^2">, we can rewrite this as <img src="https://render.githubusercontent.com/render/math?math=O(m\log{n^2}) = O(m\log{n})">.
* We start with <img src="https://render.githubusercontent.com/render/math?math=n"> isolated vertices which will be merged into connected components until all vertices belong to a single connected component. We use the Union-Find data structure to keep track of the connected components.
* For each edge <img src="https://render.githubusercontent.com/render/math?math=e = (u, v)"> on the sorted list of edges, we use two <img src="https://render.githubusercontent.com/render/math?math=\text{Find}"> operations to determine whether vertices <img src="https://render.githubusercontent.com/render/math?math=u"> and <img src="https://render.githubusercontent.com/render/math?math=v"> belong to the same component. If not, i.e. if <img src="https://render.githubusercontent.com/render/math?math=\text{Find}(u) = i"> and <img src="https://render.githubusercontent.com/render/math?math=\text{Find}(v) = j"> where <img src="https://render.githubusercontent.com/render/math?math=i \neq j">, we add edge <img src="https://render.githubusercontent.com/render/math?math=e = (u, v)"> to the spanning tree being constructed and perform <img src="https://render.githubusercontent.com/render/math?math=\text{Union}(i, j)"> to merge the connected components containing <img src="https://render.githubusercontent.com/render/math?math=u"> and <img src="https://render.githubusercontent.com/render/math?math=v">.
* We perform <img src="https://render.githubusercontent.com/render/math?math=2m"> <img src="https://render.githubusercontent.com/render/math?math=\text{Find}"> operations, each costing <img src="https://render.githubusercontent.com/render/math?math=O(1)">, as well as <img src="https://render.githubusercontent.com/render/math?math=n - 1"> <img src="https://render.githubusercontent.com/render/math?math=\text{Union}"> operations which in total cost <img src="https://render.githubusercontent.com/render/math?math=O(n\log{n})">.
* The initial sorting of the edges dominates so <img src="https://render.githubusercontent.com/render/math?math=O(m\log{n})"> is the overall time complexity.

## Dynamic Programming

* The idea is to solve a large problem recursively by building from (carefully chosen) subproblems of smaller size.
* **Optimal substructure property.** We must choose subproblems so that the optimal solutions to the subproblems can be combined into an optimal solution for the full problem.
* Greedy algorithms view a problem as a sequence of stages and we consider only the locally optimal choice at each stage. Some greedy algorithms are incorrect and fail to construct a globally optimal solution. Also, greedy algorithms are unhelpful for certain types of problems, such as "count the number of ways to ...". Dynamic programming can be used to efficiently consider all the options at each stage.
* Divide and conquer used recursion to break a large problem into *disjoint* subproblems. However, dynamic programming is charcaterised by *overlapping subproblems*.
* **Overlapping subproblems property.** We must choose subproblems so that the same subproblem occurs several times in the recursion tree. When we solve a subproblem, we *store the result* so that subsequent instances of the same subproblem can be answered by just looking up a value in a table.
* A dynamic programming algorithm consists of three parts:
    - A definition of the **subproblems**,
    - A **recurrence relation**, which determines how the solutions to smaller subproblems are combined to solve a larger subproblem, and
    - Any **base cases**, which are the trivial subproblems - those for which the recurrence is not required.
* The original problem may be one of our subproblems, or it may be solved by combining results from several subproblems, in which case we must also describe this process.
* The **time complexity** of our algorithm is usually given by multiplying the *number of subproblems* by the *average time taken to solve a subproblem using the recurrence*.
* **See the example problems in [Lectures 9-11](resources/7-dp.pdf).**
* **Notation.** <img src="https://render.githubusercontent.com/render/math?math=\underset{1 \leq m \leq n}{\argmin} \ \text{opt}(i - v_m)"> is the value of <img src="https://render.githubusercontent.com/render/math?math=m"> that minimises <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(i - v_m)">. We also have <img src="https://render.githubusercontent.com/render/math?math=\argmax">.

### Single Source Shortest Paths II

* Suppose we have a directed weighted graph <img src="https://render.githubusercontent.com/render/math?math=G = (V, E)"> with edge weights <img src="https://render.githubusercontent.com/render/math?math=w(e)"> which **can be negative**, but without cycles of negative total weight, and a (source) vertex <img src="https://render.githubusercontent.com/render/math?math=s \in V">.
* We want to find the weight of the shortest path from vertex <img src="https://render.githubusercontent.com/render/math?math=s"> to every other vertex <img src="https://render.githubusercontent.com/render/math?math=t">.
* This differs to the SSSP problem solved by **Dijkstra's algorithm** because we allow **negative edge weights**, so the greedy strategy no longer works.
* We disallow cycles of negative total weight because with such a cycle, there is no shortest path. You can take as many laps around a negative cycle as you like.

#### Bellman-Ford Algorithm

> For any vertex <img src="https://render.githubusercontent.com/render/math?math=t">, there is a shortest <img src="https://render.githubusercontent.com/render/math?math=s \rightarrow t"> path without cycles.
>
> It follows that every shortest <img src="https://render.githubusercontent.com/render/math?math=s \rightarrow t"> path contains any vertex <img src="https://render.githubusercontent.com/render/math?math=v"> at most once, and therefore has at most <img src="https://render.githubusercontent.com/render/math?math=|V| - 1"> edges.

* For every vertex <img src="https://render.githubusercontent.com/render/math?math=t">, let us find the weight of a shortest <img src="https://render.githubusercontent.com/render/math?math=s \rightarrow t"> path consisting of at most <img src="https://render.githubusercontent.com/render/math?math=i"> edges, for each <img src="https://render.githubusercontent.com/render/math?math=i"> up to <img src="https://render.githubusercontent.com/render/math?math=|V| - 1">.
* Suppose the path in question is <img src="https://render.githubusercontent.com/render/math?math=p = \underbrace{s \rightarrow \ldots \rightarrow v}_{p'} \rightarrow t">, with the final edge going from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=t">.
* Then, <img src="https://render.githubusercontent.com/render/math?math=p'"> must be itself the shortest path from <img src="https://render.githubusercontent.com/render/math?math=s"> to <img src="https://render.githubusercontent.com/render/math?math=v"> of at most <img src="https://render.githubusercontent.com/render/math?math=i - 1"> edges, which is another *subproblem*.
* No such recursion is necessary if <img src="https://render.githubusercontent.com/render/math?math=t = s"> or if <img src="https://render.githubusercontent.com/render/math?math=i = 0">.
* **Subproblems.** For all <img src="https://render.githubusercontent.com/render/math?math=0 \leq i \leq |V| - 1"> and all <img src="https://render.githubusercontent.com/render/math?math=t \in V">, let <img src="https://render.githubusercontent.com/render/math?math=P(i, t)"> be the problem of determining <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(i,t)">, the length of a shortest path from <img src="https://render.githubusercontent.com/render/math?math=s"> to <img src="https://render.githubusercontent.com/render/math?math=t"> which contains at most <img src="https://render.githubusercontent.com/render/math?math=i"> edges.
* **Recurrence.** For all <img src="https://render.githubusercontent.com/render/math?math=i > 0"> and <img src="https://render.githubusercontent.com/render/math?math=t \neq s">, <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(i, t) = \min\{\text{opt}(i - 1, v) %2B w(v,t) | (v, t) \in E\}">.
* **Base cases.** <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(i,s) = 0"> and for <img src="https://render.githubusercontent.com/render/math?math=t \neq s">, <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(0, t) = \infty">.
* The **overall solutions** are given by <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(|V| - 1, t)">.
* We proceed in <img src="https://render.githubusercontent.com/render/math?math=|V|"> rounds (<img src="https://render.githubusercontent.com/render/math?math=i = 0, 1, \ldots, |V| - 1">). In each round, each edge of the graph is considered only once. Therefore the **time complexity** is <img src="https://render.githubusercontent.com/render/math?math=O(|V||E|)">.
* This method is sometimes called **relaxation** because we progressively relax the additional constraint on how many edges the shortest paths can contain.
* The **SPFA (Shortest Paths Faster Algorithm)** speeds up the later rounds by ignoring some edges. This optimisation and others (e.g. early exit) do not change the worst case time complexity.
* The Bellman-Ford algorithm can be augmented to *detect* cycles of negative weight.

### All Pairs Shortest Paths

* Suppose we have a directed weighted graph <img src="https://render.githubusercontent.com/render/math?math=G = (V, E)"> with edge weights <img src="https://render.githubusercontent.com/render/math?math=w(e)"> which can be negative, but without cycles of negative total weight.
* We want to find the weight of the shortest path from every vertex <img src="https://render.githubusercontent.com/render/math?math=s"> to every other vertex <img src="https://render.githubusercontent.com/render/math?math=t">.

#### Floyd-Warshall Algorithm

* Label the vertices of <img src="https://render.githubusercontent.com/render/math?math=V"> as <img src="https://render.githubusercontent.com/render/math?math=v_1, v_2, \ldots, v_n"> where <img src="https://render.githubusercontent.com/render/math?math=n = |V|">.
* Let <img src="https://render.githubusercontent.com/render/math?math=S"> be the set of vertices allowed as intermediate vertices. Initially <img src="https://render.githubusercontent.com/render/math?math=S"> is empty, and we add vertices <img src="https://render.githubusercontent.com/render/math?math=v_1, v_2, \ldots, v_n"> one at a time.
* **Subproblems.** For all <img src="https://render.githubusercontent.com/render/math?math=1 \leq i, j \leq n"> and <img src="https://render.githubusercontent.com/render/math?math=0 \leq k \leq n">, let <img src="https://render.githubusercontent.com/render/math?math=P(i, j, k)"> be the problem of determining <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(i, j, k)">, the weight of a shortest path from <img src="https://render.githubusercontent.com/render/math?math=v_i"> to <img src="https://render.githubusercontent.com/render/math?math=v_j"> using only <img src="https://render.githubusercontent.com/render/math?math=v_1, \ldots, v_k"> as intermediate vertices.
* **Recurrence.** For all <img src="https://render.githubusercontent.com/render/math?math=1 \leq i, j, k \leq n">, <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(i, j, k) = \min(\text{opt}(i,j,k-1), \text{opt}(i, k, k - 1) %2B \text{opt}(k, j, k - 1))">.
* **Base cases.** <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(i, j, 0) = \begin{cases}0 %26 \text{if } i = j \\ w(i, j) %26 \text{if } (v_i, v_j) \in E \\ \infty %26 \text{otherwise}\end{cases}">.
* The **overall solutions** are given by <img src="https://render.githubusercontent.com/render/math?math=\text{opt}(i, j, n)">, where all vertices are allowed as intermediates.
* Each of <img src="https://render.githubusercontent.com/render/math?math=O(|V|^3)"> subproblems is solved in constant time, so the **time complexity** is <img src="https://render.githubusercontent.com/render/math?math=O(|V|^3)">.

## Maximum Flow

### Flow Networks

* A **flow network** <img src="https://render.githubusercontent.com/render/math?math=G = (V, E)"> is a directed graph in which each edge <img src="https://render.githubusercontent.com/render/math?math=e = (u, v) \in E"> has a *positive integer* capacity <img src="https://render.githubusercontent.com/render/math?math=c(u, v) > 0">.
* There are two distinguished vertices: a **source** <img src="https://render.githubusercontent.com/render/math?math=s"> and a **sink** <img src="https://render.githubusercontent.com/render/math?math=t">; no edge leaves the sink and no edge enters the source.

![flow-network](images/flow-network.png)

* Examples of flow networks (possibly with several sources and sinks):
    - Transportation networks
    - Gas pipelines
    - Computer networks
* A **flow** in <img src="https://render.githubusercontent.com/render/math?math=G"> is a function <img src="https://render.githubusercontent.com/render/math?math=f : E \rightarrow \mathbb{R}^{%2B}, f(u, v) \geq 0">, which satisfies:
    1. **Capacity constraint:** for all edges <img src="https://render.githubusercontent.com/render/math?math=e = (u, v) \in E"> we require <img src="https://render.githubusercontent.com/render/math?math=f(u, v) \leq c(u, v)">, i.e. the flow through any edge does not exceed its capacity.
    2. **Flow conservation:** for all vertices <img src="https://render.githubusercontent.com/render/math?math=v \in S - \{s, t\}"> we require <img src="https://render.githubusercontent.com/render/math?math=\underset{(u,v) \in E}{\sum} f(u,v) = \underset{(v,w) \in E}{\sum}f(v,w)">, i.e. the flow into any vertex (other than the source and the sink) equals the flow out of that vertex.
* The **value** of a flow is defined as <img src="https://render.githubusercontent.com/render/math?math=|f| = \underset{v:(s,v) \in E}{\sum}f(s,v) = \underset{v:(v,t) \in E}{\sum}f(v,t)">, i.e. the flow leaving the source or equivalently the flow arriving at the sink.
* Given a flow network, our goal is to find a flow of maximum value.

> **Integrality Theorem.** If all capacities are integers (as assumed earlier), then there is a flow of maximum value such that <img src="https://render.githubusercontent.com/render/math?math=f(u,v)"> is an integer for each edge <img src="https://render.githubusercontent.com/render/math?math=(u,v) \in E">.

### Residual Flow Networks

* Given a flow in a flow network, the **residual flow network** is the network made up of the leftover capacities.

![flow-network](images/flow-network-1.png)
![residual-flow-network](images/residual-flow-network.png)

* Suppose the original flow network has an edge from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w"> with capacity <img src="https://render.githubusercontent.com/render/math?math=c">, and that <img src="https://render.githubusercontent.com/render/math?math=f"> units of flow are being sent through this edge.
* The residual flow network has two edges:
    1. an edge from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w"> with capacity <img src="https://render.githubusercontent.com/render/math?math=c - f">, and
    2. an edge from <img src="https://render.githubusercontent.com/render/math?math=w"> to <img src="https://render.githubusercontent.com/render/math?math=v"> with capacity <img src="https://render.githubusercontent.com/render/math?math=f">.
* These capacities represent the amount of additional flow in each direction. Note that sending flow on the "virtual" edge from <img src="https://render.githubusercontent.com/render/math?math=w"> to <img src="https://render.githubusercontent.com/render/math?math=v"> counteracts the already assigned flow from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w">.
* Edges of capacity zero (when <img src="https://render.githubusercontent.com/render/math?math=f = 0"> or <img src="https://render.githubusercontent.com/render/math?math=f = c">) need not be included.
* Suppose the original flow network has an edge from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w"> with capacity <img src="https://render.githubusercontent.com/render/math?math=c_1"> and flow <img src="https://render.githubusercontent.com/render/math?math=f_1"> units, *and* an edge from <img src="https://render.githubusercontent.com/render/math?math=w"> to <img src="https://render.githubusercontent.com/render/math?math=v"> with capacity <img src="https://render.githubusercontent.com/render/math?math=c_2"> and flow <img src="https://render.githubusercontent.com/render/math?math=f_2"> units.
* In this case, the residual flow network has edges:
    1. an edge from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w"> with capacity <img src="https://render.githubusercontent.com/render/math?math=c_1 - f_1 %2B f_2">, and
    2. an edge from <img src="https://render.githubusercontent.com/render/math?math=w"> to <img src="https://render.githubusercontent.com/render/math?math=v"> with capacity <img src="https://render.githubusercontent.com/render/math?math=c_2 - f_2 %2B f_1">.
* This is because from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w">, the forward edge allows <img src="https://render.githubusercontent.com/render/math?math=c_1 - f_1"> additional units of flow, and we can also send up to <img src="https://render.githubusercontent.com/render/math?math=f_2"> units to cancel the flow through the reverse edge.

### Augmenting Paths

* An **augmenting path** is a path from <img src="https://render.githubusercontent.com/render/math?math=s"> to <img src="https://render.githubusercontent.com/render/math?math=t"> in the residual flow network.

![augmenting-path](images/augmenting-path.png)

* The **capacity** of an augmenting path is the capacity of its "bottleneck" edge, i.e. the edge of smallest capacity.
* We can now send that amount of flow along the augmenting path, recalculating the flow and the residual capacities for each edge used.
* Suppose we have an augmenting path of capacity <img src="https://render.githubusercontent.com/render/math?math=f">, including an edge from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w">. We should:
    - cancel up to <img src="https://render.githubusercontent.com/render/math?math=f"> units of flow being sent from <img src="https://render.githubusercontent.com/render/math?math=w"> to <img src="https://render.githubusercontent.com/render/math?math=v">,
    - add the remainder of these <img src="https://render.githubusercontent.com/render/math?math=f"> units to the flow being sent from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w">,
    - increase the residual capacity from <img src="https://render.githubusercontent.com/render/math?math=w"> to <img src="https://render.githubusercontent.com/render/math?math=v"> by <img src="https://render.githubusercontent.com/render/math?math=f">, and
    - reduce the residual capacity from <img src="https://render.githubusercontent.com/render/math?math=v"> to <img src="https://render.githubusercontent.com/render/math?math=w"> by <img src="https://render.githubusercontent.com/render/math?math=f">.
* For the above augmenting path, after sending 4 units of flow along this path, the new residual flow network becomes:

![augmenting-path](images/augmenting-path-1.png)

### Solving the Maximum Flow Problem

#### Ford-Fulkerson Algorithm

> * Keep adding flow through new augmenting paths for as long as it is possible.
> * When there are no more augmenting paths, you have achieved the largest possible flow in the network.

* The proof is based on the notion of a **minimal cut in a flow network**.
* A **cut** in a flow network is any partition of the vertices of the underlying graph into two subsets <img src="https://render.githubusercontent.com/render/math?math=S"> and <img src="https://render.githubusercontent.com/render/math?math=T"> such that:
    1. <img src="https://render.githubusercontent.com/render/math?math=S \cup T = V">
    2. <img src="https://render.githubusercontent.com/render/math?math=S \cap T = \varnothing">
    3. <img src="https://render.githubusercontent.com/render/math?math=s \in S"> and <img src="https://render.githubusercontent.com/render/math?math=t \in T">
* The **capacity** <img src="https://render.githubusercontent.com/render/math?math=c(S, T)"> of a cut <img src="https://render.githubusercontent.com/render/math?math=(S, T)"> is the sum of all the capacities of all edges leaving <img src="https://render.githubusercontent.com/render/math?math=S"> and entering <img src="https://render.githubusercontent.com/render/math?math=T">, i.e. <img src="https://render.githubusercontent.com/render/math?math=c(S, T) = \underset{(u,v) \in E}{\sum} \{c(u,v) : u \in S, v \in T\}">. Note that capacities of edges going in the opposite direction (from <img src="https://render.githubusercontent.com/render/math?math=T"> to <img src="https://render.githubusercontent.com/render/math?math=S">) do not count.
* Given a flow <img src="https://render.githubusercontent.com/render/math?math=f">, the **flow** <img src="https://render.githubusercontent.com/render/math?math=f(S, T)"> through a cut <img src="https://render.githubusercontent.com/render/math?math=(S,T)"> is the total flow through edges from <img src="https://render.githubusercontent.com/render/math?math=S"> to <img src="https://render.githubusercontent.com/render/math?math=T"> minus the total flow through edges from <img src="https://render.githubusercontent.com/render/math?math=T"> to <img src="https://render.githubusercontent.com/render/math?math=S">, i.e. <img src="https://render.githubusercontent.com/render/math?math=f(S,T) = \underset{(u,v) \in E}{\sum} \{f(u,v) : u \in S, v \in T\} - \underset{(u,v) \in E}{\sum} \{f(u,v) : u \in T, v \in S\}">.

> For any flow <img src="https://render.githubusercontent.com/render/math?math=f">, the flow through any cut <img src="https://render.githubusercontent.com/render/math?math=(S,T)"> is equal to the value of the flow, i.e. <img src="https://render.githubusercontent.com/render/math?math=f(S, T) = |f|">.

* An edge from <img src="https://render.githubusercontent.com/render/math?math=S"> to <img src="https://render.githubusercontent.com/render/math?math=T"> counts its full capacity towards <img src="https://render.githubusercontent.com/render/math?math=c(S,T)">, but only the flow through it towards <img src="https://render.githubusercontent.com/render/math?math=f(S,T)">.
* An edge from <img src="https://render.githubusercontent.com/render/math?math=T"> to <img src="https://render.githubusercontent.com/render/math?math=S"> counts zero towards <img src="https://render.githubusercontent.com/render/math?math=c(S,T)">, but minuses the flow through it from <img src="https://render.githubusercontent.com/render/math?math=f(S,T)">.
* Therefore, <img src="https://render.githubusercontent.com/render/math?math=f(S,T) \leq c(S,T)">.
* It follows that <img src="https://render.githubusercontent.com/render/math?math=|f| \leq c(S,T)">, so the value of any flow is at most the capacity of any cut.

![cuts-flow-network](images/cuts-flow-network.png)

* In this example, <img src="https://render.githubusercontent.com/render/math?math=f(S,T) = f(v_1, v_3) %2B f(v_2, v_4) - f(v_2, v_3) = 12 %2B 11 - 4 = 19"> and <img src="https://render.githubusercontent.com/render/math?math=c(S,T) = c(v_1, v_3) %2B c(v_2, v_4) = 12 %2B 14 = 26">.

> **Max Flow Min Cut Theorem.** The maximal amount of flow in a flow network is equal to the capacity of the cut of minimal capacity.

* Since <img src="https://render.githubusercontent.com/render/math?math=|f|"> is at most <img src="https://render.githubusercontent.com/render/math?math=c(S,T)">, then if we find a flow <img src="https://render.githubusercontent.com/render/math?math=f"> which equals the capacity of some cut <img src="https://render.githubusercontent.com/render/math?math=(S,T)">, then such flow must be maximal and the capacity of such a cut must be minimal.

> Assume that the Ford-Fulkerson algorithm has terminated. Define <img src="https://render.githubusercontent.com/render/math?math=S"> to be the source <img src="https://render.githubusercontent.com/render/math?math=s"> and all vertices <img src="https://render.githubusercontent.com/render/math?math=u"> such that there is a path in the residual flow network from <img src="https://render.githubusercontent.com/render/math?math=s"> to <img src="https://render.githubusercontent.com/render/math?math=u">. Define <img src="https://render.githubusercontent.com/render/math?math=T"> to be the set of all vertices for which there is no such path. Since there are no more augmenting paths from <img src="https://render.githubusercontent.com/render/math?math=s"> to <img src="https://render.githubusercontent.com/render/math?math=t">, then the sink <img src="https://render.githubusercontent.com/render/math?math=t"> belongs to <img src="https://render.githubusercontent.com/render/math?math=T">.
>
> All the edges from <img src="https://render.githubusercontent.com/render/math?math=S"> to <img src="https://render.githubusercontent.com/render/math?math=T"> are fully occupied with flow, and all the edges from <img src="https://render.githubusercontent.com/render/math?math=T"> to <img src="https://render.githubusercontent.com/render/math?math=S"> are empty **(proof omitted)**.

![ford-fulkerson](images/ford-fulkerson.png)

* Since all edges from <img src="https://render.githubusercontent.com/render/math?math=S"> to <img src="https://render.githubusercontent.com/render/math?math=T"> are occupied with flows to their full capacity, and also there is no flow from <img src="https://render.githubusercontent.com/render/math?math=T"> to <img src="https://render.githubusercontent.com/render/math?math=S">, then <img src="https://render.githubusercontent.com/render/math?math=f(S,T) = c(S,T) = |f|">. Thus, such a flow is maximal and the corresponding cut is a minimal cut.
* The Ford-Fulkerson algorithm can potentially run in **time proportional to the value of the max flow**, which can be **exponential in the size of the input**.
* In a flow network, <img src="https://render.githubusercontent.com/render/math?math=|V| \leq |E| %2B 1"> otherwise there are vertices other than the source which don't have any incoming edges, or vertices other than the sink which don't have any outgoing edges. We therefore simplify <img src="https://render.githubusercontent.com/render/math?math=O(|V| %2B |E|)"> to <img src="https://render.githubusercontent.com/render/math?math=O(|E|)">.
* The Ford-Fulkerson algorithm has worst-case time complexity of <img src="https://render.githubusercontent.com/render/math?math=O(|E|f)"> where <img src="https://render.githubusercontent.com/render/math?math=f"> is the value of a maximum flow. In general if there are <img src="https://render.githubusercontent.com/render/math?math=m"> edges in the graph, each of capacity <img src="https://render.githubusercontent.com/render/math?math=C">, then <img src="https://render.githubusercontent.com/render/math?math=f"> may be up to <img src="https://render.githubusercontent.com/render/math?math=mC">. Since the edge capacities are specified using only <img src="https://render.githubusercontent.com/render/math?math=m\log_{2}{C}"> bits, the algorithm does not run in polynomial time in general.
* In some circumstances the time complexity of the Ford-Fulkerson algorithm is <img src="https://render.githubusercontent.com/render/math?math=O(|E||V|)">.

#### Edmonds-Karp Algorithm

* The Edmonds-Karp algorithm improves the Ford-Fulkerson algorithm in a simple way: always choose the shortest path from the source <img src="https://render.githubusercontent.com/render/math?math=s"> to the sink <img src="https://render.githubusercontent.com/render/math?math=t">, where the "shortest path" means the fewest number of edges, regardless of their capacities.
* This algorithm runs in <img src="https://render.githubusercontent.com/render/math?math=O(|V||E|^2)"> time.
* The **fastest** max flow algorithm to date is an extension of the **Preflow-Push** algorithm and runs in time <img src="https://render.githubusercontent.com/render/math?math=|V|^3">.
* The Edmonds-Karp algorithm is a specialisation of the Ford-Fulkerson algorithm, so its time complexity is also bounded by <img src="https://render.githubusercontent.com/render/math?math=O(|E|f)">. It can be proved that it finds <img src="https://render.githubusercontent.com/render/math?math=O(|V||E|)"> augmenting paths, each in <img src="https://render.githubusercontent.com/render/math?math=O(|E|)"> time using BFS, so an alternative bound for its time complexity is <img src="https://render.githubusercontent.com/render/math?math=O(|V||E|^2)">.
* The time complexity can be written <img src="https://render.githubusercontent.com/render/math?math=O(\min(|V||E|^2, |E|f))">.

### Applications of Network Flow

* Flow networks with **multiple sources and sinks** are reducible to networks with a single source and single sink by adding a **super-source** and **super-sink** and connecting them to all sources and sinks respectively by edges of *infinite capacity*.

![multiple-sources-sinks](images/multiple-sources-sinks.png)

* Sometimes not only the edges but also the **vertices <img src="https://render.githubusercontent.com/render/math?math=v_i"> of the flow graph might have capacities <img src="https://render.githubusercontent.com/render/math?math=C(v_i)">** which limit the total throughput of the flow coming to the vertex and leaving the vertex: <img src="https://render.githubusercontent.com/render/math?math=\underset{(u,v) \in E}{\sum}f(u,v) = \underset{(v,w) \in E}{\sum}f(v, w) \leq C(v)">.
* We can also reduce this to a situation with **only edge capacities**. Suppose vertex <img src="https://render.githubusercontent.com/render/math?math=v"> has capacity <img src="https://render.githubusercontent.com/render/math?math=C(v)">. Split <img src="https://render.githubusercontent.com/render/math?math=v"> into two vertices <img src="https://render.githubusercontent.com/render/math?math=v_{in}"> and <img src="https://render.githubusercontent.com/render/math?math=v_{out}">. Attach all of <img src="https://render.githubusercontent.com/render/math?math=v">'s incoming edges to <img src="https://render.githubusercontent.com/render/math?math=v_{in}"> and all its outgoing edges from <img src="https://render.githubusercontent.com/render/math?math=v_{out}">. Connect <img src="https://render.githubusercontent.com/render/math?math=v_{in}"> and <img src="https://render.githubusercontent.com/render/math?math=v_{out}"> with an edge <img src="https://render.githubusercontent.com/render/math?math=e^* = (v_{in}, v_{out})"> of capacity <img src="https://render.githubusercontent.com/render/math?math=C(v)">.

![vertex-capacities](images/vertex-capacities.png)

### Bipartite Graphs

> A graph <img src="https://render.githubusercontent.com/render/math?math=G = (V, E)"> is said to be **bipartite** if its vertices can be divided into two disjoint sets <img src="https://render.githubusercontent.com/render/math?math=A"> and <img src="https://render.githubusercontent.com/render/math?math=B"> such that every edge <img src="https://render.githubusercontent.com/render/math?math=e \in E"> has one end in the set <img src="https://render.githubusercontent.com/render/math?math=A"> and the other in the set <img src="https://render.githubusercontent.com/render/math?math=B">.

* A **matching** in a graph <img src="https://render.githubusercontent.com/render/math?math=G = (V, E)"> is a subset <img src="https://render.githubusercontent.com/render/math?math=M \subseteq E"> such that each vertex of the graph belongs to at most one edge in <img src="https://render.githubusercontent.com/render/math?math=M">.
* A **maximum matching** in <img src="https://render.githubusercontent.com/render/math?math=G"> is a matching containing the largest possible number of edges.

![matchings-bipartite](images/matchings-bipartite.png)

* We can turn a **Maximum Bipartite Matching** problem into a **Maximum Flow** problem: Create two new vertices <img src="https://render.githubusercontent.com/render/math?math=s"> and <img src="https://render.githubusercontent.com/render/math?math=t"> (the source and sink). Construct an edge from <img src="https://render.githubusercontent.com/render/math?math=s"> to each vertex in <img src="https://render.githubusercontent.com/render/math?math=A">, and from each vertex in <img src="https://render.githubusercontent.com/render/math?math=B"> to <img src="https://render.githubusercontent.com/render/math?math=t">. Orient the existing edges from <img src="https://render.githubusercontent.com/render/math?math=A"> to <img src="https://render.githubusercontent.com/render/math?math=B">. Assign capacity 1 to all edges.
* Since all capacities in the flow network are 1, we need only denote the *direction* of the edge in the residual graph.

![max-bipartite-matching](images/max-bipartite-matching.png)
![max-bipartite-matching](images/max-bipartite-matching-1.png)

## String Matching

* Suppose you have an alphabet <img src="https://render.githubusercontent.com/render/math?math=S = \{s_0, s_1, \ldots, s_{d-1}\}"> of <img src="https://render.githubusercontent.com/render/math?math=d"> characters.
* You want to determine whether a string <img src="https://render.githubusercontent.com/render/math?math=B = b_0 b_1 \ldots b_{m-1}"> appears as a *contiguous* substring of a much longer string <img src="https://render.githubusercontent.com/render/math?math=A = a_0 a_1 \ldots a_{n-1}">.
* The *naive* string matching algorithm runs in <img src="https://render.githubusercontent.com/render/math?math=O(nm)">.

### Hashing

#### Rabin-Karp Algorithm

* We compute a hash value for the string <img src="https://render.githubusercontent.com/render/math?math=B = b_0 b_1 b_2 \ldots b_{m-1}"> in the following way:
    - First, map each symbol <img src="https://render.githubusercontent.com/render/math?math=s_i"> to a corresponding integer <img src="https://render.githubusercontent.com/render/math?math=i">: <img src="https://render.githubusercontent.com/render/math?math=S = \{s_0, s_1, s_2, \ldots, s_{d-1}\} \rightarrow \{0, 1, 2, \ldots, d-1\}">, so as to identify each string with a sequence of these integers.
    - Then, when we refer to an integer <img src="https://render.githubusercontent.com/render/math?math=a_i"> or <img src="https://render.githubusercontent.com/render/math?math=b_i">, we refer to the ID of the symbol <img src="https://render.githubusercontent.com/render/math?math=a_i"> or <img src="https://render.githubusercontent.com/render/math?math=b_i">.
    - We can therefore identify <img src="https://render.githubusercontent.com/render/math?math=B"> with a sequence of IDs <img src="https://render.githubusercontent.com/render/math?math=\langle b_0, b_1, b_2, \ldots, b_{m-1} \rangle">, each between 0 and <img src="https://render.githubusercontent.com/render/math?math=d-1"> inclusive. Viewing these IDs as digits in base <img src="https://render.githubusercontent.com/render/math?math=d">, we can construct a corresponding integer <img src="https://render.githubusercontent.com/render/math?math=h(B) = h(b_0 b_1 b_2 \ldots b_{m-1}) = d^{m-1}b_0 %2B d^{m-2}b_1 %2B \ldots %2B db_{m-2} %2B b_{m-1}">.
    - This can be evaluated efficiently using **Horner's rule**: <img src="https://render.githubusercontent.com/render/math?math=h(B) = b_{m-1} %2B d(b_{m-2} %2B d(b_{m-3} %2B d(b_{m-4} %2B \ldots %2B d(b_1 %2B db_0)\ldots)))">, requiring only <img src="https://render.githubusercontent.com/render/math?math=m-1"> additions and <img src="https://render.githubusercontent.com/render/math?math=m-1"> multiplications.
    - Next we choose a large prime number <img src="https://render.githubusercontent.com/render/math?math=p"> and define the hash value of <img src="https://render.githubusercontent.com/render/math?math=B"> as <img src="https://render.githubusercontent.com/render/math?math=H(B) = h(B) \mod{p}">. We require that <img src="https://render.githubusercontent.com/render/math?math=(d%2B1)p"> fits in a register.
* Recall that <img src="https://render.githubusercontent.com/render/math?math=A = a_0 a_1 a_2 a_3 \ldots a_s a_{s%2B1} \ldots a_{s%2Bm-1} \ldots a_{n-1}"> where <img src="https://render.githubusercontent.com/render/math?math=n \gg m">.
* We want to efficiently find all <img src="https://render.githubusercontent.com/render/math?math=s"> such that the string of length <img src="https://render.githubusercontent.com/render/math?math=m"> of the form <img src="https://render.githubusercontent.com/render/math?math=a_s a_{s%2B1} \ldots a_{s%2Bm-1}"> and string <img src="https://render.githubusercontent.com/render/math?math=b_0 b_1 \ldots b_{m-1}"> are equal.
* For each contiguous substring <img src="https://render.githubusercontent.com/render/math?math=A_s = a_s a_{s%2B1} \ldots a_{s%2Bm-1}"> of string <img src="https://render.githubusercontent.com/render/math?math=A"> we also compute its hash value as <img src="https://render.githubusercontent.com/render/math?math=H(A_s) = d^{m-1} a_s %2B d^{m-2} a_{s%2B1} %2B \ldots %2B d^1 a_{s%2Bm-2} %2B a_{s%2Bm-1} \mod{p}">.
* We can now compare the hash values <img src="https://render.githubusercontent.com/render/math?math=H(B)"> and <img src="https://render.githubusercontent.com/render/math?math=H(A_s)"> and do a symbol-by-symbol matching only if <img src="https://render.githubusercontent.com/render/math?math=H(B) = H(A_s)">.
* Such an algorithm would only be faster than the naive symbol-by-symbol comparison only if we can compute the hash values of substrings <img src="https://render.githubusercontent.com/render/math?math=A_s"> faster than comparing strings <img src="https://render.githubusercontent.com/render/math?math=B"> and <img src="https://render.githubusercontent.com/render/math?math=A_s"> character by character.
* We use **recursion**: we compute <img src="https://render.githubusercontent.com/render/math?math=H(A_{s%2B1})"> efficiently from <img src="https://render.githubusercontent.com/render/math?math=H(A_s)"> by doing the following:
    - Since <img src="https://render.githubusercontent.com/render/math?math=H(A_s) = d^{m-1} a_s %2B d^{m-2} a_{s%2B1} %2B \ldots %2B d^1 a_{s%2Bm-2} %2B a_{s%2Bm-1} \mod{p}">, then by multiplying both sides by <img src="https://render.githubusercontent.com/render/math?math=d"> we obtain <img src="https://render.githubusercontent.com/render/math?math=\begin{align*} d %26 \cdot H(A_s) \\ %26= d^m a_s %2B d^{m-1}a_{s%2B1} %2B \ldots %2B d^1 a_{s%2Bm-1} \\ %26=  d^m a_s %2B (d^{m-1} a_{s%2B1} %2B \ldots %2B d^1 a_{s%2Bm-1} %2B a_{s%2Bm}) - a_{s%2Bm} \\ %26= d^m a_s %2B H(A_{s%2B1}) - a_{s%2Bm} \mod{p} \end{align*}">
    - Consequently, <img src="https://render.githubusercontent.com/render/math?math=H(A_{s%2B1}) = d \cdot H(A_s) - d^m a_s %2B a_{s%2Bm} \mod{p}">.
    - To find <img src="https://render.githubusercontent.com/render/math?math=d^m a_s \mod{p}">, we use the precomputed value <img src="https://render.githubusercontent.com/render/math?math=d^m \mod{p}">, multiply it by <img src="https://render.githubusercontent.com/render/math?math=a_s"> and again take the remainder modulo <img src="https://render.githubusercontent.com/render/math?math=p">.
    - Also, since <img src="https://render.githubusercontent.com/render/math?math=(-d^m a_s %2B a_{s%2Bm}) \mod{p}"> and <img src="https://render.githubusercontent.com/render/math?math=H(A_s)"> are each less than <img src="https://render.githubusercontent.com/render/math?math=p">, it follows that <img src="https://render.githubusercontent.com/render/math?math=d \cdot H(A_s) %2B [(-d^m a_s %2B a_{s%2Bm}) \mod{p}] < (d%2B1)p">.
    - Thus, since we chose <img src="https://render.githubusercontent.com/render/math?math=p"> such that <img src="https://render.githubusercontent.com/render/math?math=(d%2B1)p"> fits in a single register, all the values and the intermediate results for the above expression also fit in a single register.
* Thus, we first compute <img src="https://render.githubusercontent.com/render/math?math=H(B)"> and <img src="https://render.githubusercontent.com/render/math?math=H(A_0)"> using Horner's rule.
* The <img src="https://render.githubusercontent.com/render/math?math=O(n)"> subsequent values of <img src="https://render.githubusercontent.com/render/math?math=H(A_s)"> for <img src="https://render.githubusercontent.com/render/math?math=s > 0"> are computed in constant time using the above recursion.
* <img src="https://render.githubusercontent.com/render/math?math=H(A_s)"> is compared with <img src="https://render.githubusercontent.com/render/math?math=H(B)"> and if they are equal the strings <img src="https://render.githubusercontent.com/render/math?math=A_s"> and <img src="https://render.githubusercontent.com/render/math?math=B"> are compared by brute force character-by-character to confirm whether they are genuinely equal.
* Since <img src="https://render.githubusercontent.com/render/math?math=p"> was chosen large, the false positives when <img src="https://render.githubusercontent.com/render/math?math=H(A_s) = H(B)"> but <img src="https://render.githubusercontent.com/render/math?math=A_s \neq B"> are very unlikely, which makes the algorithm **run fast in the average case**.
* However, when we use hashing we cannot achieve useful bounds for the worst case performance.

### Finite Automata

* A string matching finite automaton for a pattern <img src="https://render.githubusercontent.com/render/math?math=B"> of length <img src="https://render.githubusercontent.com/render/math?math=m"> has:
    - <img src="https://render.githubusercontent.com/render/math?math=m%2B1"> many states <img src="https://render.githubusercontent.com/render/math?math=0, 1, \ldots, m"> which correspond to the number of characters matched thus far, and
    - a transition function <img src="https://render.githubusercontent.com/render/math?math=\delta (s,c)"> where <img src="https://render.githubusercontent.com/render/math?math=0 \leq s \leq m"> and <img src="https://render.githubusercontent.com/render/math?math=c \in S">. <img src="https://render.githubusercontent.com/render/math?math=\delta (s,c)"> is the state you go to if you were in state <img src="https://render.githubusercontent.com/render/math?math=s"> and then saw a character <img src="https://render.githubusercontent.com/render/math?math=c">.
* Suppose that the last <img src="https://render.githubusercontent.com/render/math?math=s"> characters of the text <img src="https://render.githubusercontent.com/render/math?math=A"> match the first <img src="https://render.githubusercontent.com/render/math?math=s"> characters of the pattern <img src="https://render.githubusercontent.com/render/math?math=B">, and that <img src="https://render.githubusercontent.com/render/math?math=c"> is the next character in the text. Then <img src="https://render.githubusercontent.com/render/math?math=\delta (s,c)"> is the new state after character <img src="https://render.githubusercontent.com/render/math?math=c"> is read, i.e. the largest <img src="https://render.githubusercontent.com/render/math?math=s'"> so that the last <img src="https://render.githubusercontent.com/render/math?math=s'"> characters of <img src="https://render.githubusercontent.com/render/math?math=A"> (ending at the new character <img src="https://render.githubusercontent.com/render/math?math=c">) match the first <img src="https://render.githubusercontent.com/render/math?math=s'"> characters of <img src="https://render.githubusercontent.com/render/math?math=B">.
* We first suppose that <img src="https://render.githubusercontent.com/render/math?math=\delta (s,c)"> is given as a pre-constructed table. For example, if <img src="https://render.githubusercontent.com/render/math?math=B = xyxyxzx">, then the table defining <img src="https://render.githubusercontent.com/render/math?math=\delta (s,c)"> would be:

![string-matching-finite-automata](images/string-matching-finite-automata.png)
![string-matching-finite-automata](images/string-matching-finite-automata-1.png)

* To compute the transition function <img src="https://render.githubusercontent.com/render/math?math=\delta"> (this table):
    - Let <img src="https://render.githubusercontent.com/render/math?math=B_k = b_0 \ldots b_{k-1}"> denote a prefix of length <img src="https://render.githubusercontent.com/render/math?math=k"> of the string <img src="https://render.githubusercontent.com/render/math?math=B">.
    - Being at state <img src="https://render.githubusercontent.com/render/math?math=k"> means that so far we have matched the prefix <img src="https://render.githubusercontent.com/render/math?math=B_k">.
    - If we now see an input character <img src="https://render.githubusercontent.com/render/math?math=a">, then <img src="https://render.githubusercontent.com/render/math?math=\delta (k, a)"> is the largest <img src="https://render.githubusercontent.com/render/math?math=m"> such that the prefix <img src="https://render.githubusercontent.com/render/math?math=B_m"> of string <img src="https://render.githubusercontent.com/render/math?math=B"> is a suffix of the string <img src="https://render.githubusercontent.com/render/math?math=B_k a">.
    - In the particular case where <img src="https://render.githubusercontent.com/render/math?math=a = b_k">, i.e. <img src="https://render.githubusercontent.com/render/math?math=B_k a = B_{k%2B1}">, then <img src="https://render.githubusercontent.com/render/math?math=m = k %2B 1"> and so <img src="https://render.githubusercontent.com/render/math?math=\delta (k, a) = k %2B 1">.
    - If <img src="https://render.githubusercontent.com/render/math?math=a \neq b_k"> however, we cant extend our match from length <img src="https://render.githubusercontent.com/render/math?math=k"> to <img src="https://render.githubusercontent.com/render/math?math=k%2B1">. To find <img src="https://render.githubusercontent.com/render/math?math=\delta (k, a)">, the largest <img src="https://render.githubusercontent.com/render/math?math=m"> such that <img src="https://render.githubusercontent.com/render/math?math=B_m"> is a suffix of <img src="https://render.githubusercontent.com/render/math?math=B_k a">, we match the string against itself: we can recursively compute a function <img src="https://render.githubusercontent.com/render/math?math=\pi (k)"> which for each <img src="https://render.githubusercontent.com/render/math?math=k"> returns the largest integer <img src="https://render.githubusercontent.com/render/math?math=m"> such that the prefix <img src="https://render.githubusercontent.com/render/math?math=B_m"> of <img src="https://render.githubusercontent.com/render/math?math=B"> is a proper suffix of <img src="https://render.githubusercontent.com/render/math?math=B_k">.
    - Suppose we have already found that <img src="https://render.githubusercontent.com/render/math?math=\pi (k)">, i.e. <img src="https://render.githubusercontent.com/render/math?math=B_{\pi (k)} = b_0 \ldots b_{\pi (k) - 1}"> is the longest prefix of <img src="https://render.githubusercontent.com/render/math?math=B"> which is a proper suffix of <img src="https://render.githubusercontent.com/render/math?math=B_k">.
    - To compute <img src="https://render.githubusercontent.com/render/math?math=\pi (k%2B1)">, we first check whether <img src="https://render.githubusercontent.com/render/math?math=b_k = b_{\pi (k)}">.
        * If true, then <img src="https://render.githubusercontent.com/render/math?math=\pi (k%2B1) = \pi(k) %2B 1">.
        * If false, then we cannot extend <img src="https://render.githubusercontent.com/render/math?math=B_{\pi (k)}">. The next longest prefix of <img src="https://render.githubusercontent.com/render/math?math=B"> which is a proper suffix of <img src="https://render.githubusercontent.com/render/math?math=B_k"> is <img src="https://render.githubusercontent.com/render/math?math=B_{\pi (\pi (k))}">, so we check whether <img src="https://render.githubusercontent.com/render/math?math=b_k = b_{\pi (\pi (k))}">.
            - If true, then <img src="https://render.githubusercontent.com/render/math?math=\pi (k%2B1) = \pi (\pi (k)) %2B 1">.
            - If false, then check whether <img src="https://render.githubusercontent.com/render/math?math=b_k = b_{\pi (\pi (\pi (k)))}">, and so on...

#### Knuth-Morris-Pratt Algorithm

![knuth-morris-pratt](images/knuth-morris-pratt.png)

* There are <img src="https://render.githubusercontent.com/render/math?math=O(m)"> values of <img src="https://render.githubusercontent.com/render/math?math=k">, and for each we might try several values <img src="https://render.githubusercontent.com/render/math?math=l">.
* We maintain two pointers: the left pointer <img src="https://render.githubusercontent.com/render/math?math=k %2B 1 - l"> (the start of the match we are trying to extend) and the right pointer at <img src="https://render.githubusercontent.com/render/math?math=k">.
* After each step of the algorithm (i.e. each comparison between <img src="https://render.githubusercontent.com/render/math?math=b_k"> and <img src="https://render.githubusercontent.com/render/math?math=b_l">), exactly one of these two pointers is moved forwards.
* Each can take up to <img src="https://render.githubusercontent.com/render/math?math=m"> values, so the total number of steps is <img src="https://render.githubusercontent.com/render/math?math=O(m)">. This is an example of **amortisation**.
* The **time complexity** of this algorithm is linear <img src="https://render.githubusercontent.com/render/math?math=O(m)">.
* We can now do our search for string <img src="https://render.githubusercontent.com/render/math?math=B"> in a longer string <img src="https://render.githubusercontent.com/render/math?math=A">.
* Suppose <img src="https://render.githubusercontent.com/render/math?math=B_s"> is the longest prefix of <img src="https://render.githubusercontent.com/render/math?math=B"> which is a suffix of <img src="https://render.githubusercontent.com/render/math?math=A_i = a_0 \ldots a_{i-1}">.
* To answer the same question for <img src="https://render.githubusercontent.com/render/math?math=A_{i%2B1}">, we begin by checking whether <img src="https://render.githubusercontent.com/render/math?math=a_i = b_s">.
    - If true, then the answer for <img src="https://render.githubusercontent.com/render/math?math=A_{i%2B1}"> is <img src="https://render.githubusercontent.com/render/math?math=s%2B1">.
    - If false, check whether <img src="https://render.githubusercontent.com/render/math?math=a_i = b_{\pi (s)}">...
* If the answer for any <img src="https://render.githubusercontent.com/render/math?math=A_i"> is <img src="https://render.githubusercontent.com/render/math?math=m">, we have a match.
    - Reset to state <img src="https://render.githubusercontent.com/render/math?math=\pi (m)"> to detect any overlapping full matches.
* By the same two pointer argument, the time complexity is <img src="https://render.githubusercontent.com/render/math?math=O(n)">.

![knuth-morris-pratt](images/knuth-morris-pratt-1.png)
![knuth-morris-pratt](images/knuth-morris-pratt-2.png)

#### Looking for Imperfect Matches

* Given a very long string <img src="https://render.githubusercontent.com/render/math?math=A = a_0 a_1 a_2 a_3 \ldots a_s a_{s%2B1} \ldots a_{s%2Bm-1} \ldots a_{n-1}">, a shorter string <img src="https://render.githubusercontent.com/render/math?math=B = b_0 b_1 b_2 \ldots b_{m-1}">, where <img src="https://render.githubusercontent.com/render/math?math=m \ll n">, and an integer <img src="https://render.githubusercontent.com/render/math?math=k \ll m">, we want to find all matches for <img src="https://render.githubusercontent.com/render/math?math=B"> in <img src="https://render.githubusercontent.com/render/math?math=A"> which have **up to <img src="https://render.githubusercontent.com/render/math?math=k"> errors**.
* We split <img src="https://render.githubusercontent.com/render/math?math=B"> into <img src="https://render.githubusercontent.com/render/math?math=k%2B1"> substrings of (approximately) equal length. Then any match in <img src="https://render.githubusercontent.com/render/math?math=A"> with at most <img src="https://render.githubusercontent.com/render/math?math=k"> errors must contain a substring which is a perfect match for a substring of <img src="https://render.githubusercontent.com/render/math?math=B">.
* We look for all perfect matches in <img src="https://render.githubusercontent.com/render/math?math=A"> for each of the <img src="https://render.githubusercontent.com/render/math?math=k%2B1"> parts of <img src="https://render.githubusercontent.com/render/math?math=B">. For every match, we test by brute force whether the remaining parts of <img src="https://render.githubusercontent.com/render/math?math=B"> match sufficiently with the appropriate parts of <img src="https://render.githubusercontent.com/render/math?math=A">.

## Linear Programming

* In the **standard form** the **objective** to be **maximised** is given by <img src="https://render.githubusercontent.com/render/math?math=\sum_{j=1}^n c_j x_j"> and the **constraints** are of the form:
    - <img src="https://render.githubusercontent.com/render/math?math=\sum_{j=1}^n a_{ij}x_j \leq b_i"> &nbsp;&nbsp;&nbsp; <img src="https://render.githubusercontent.com/render/math?math=(1 \leq i \leq m)">
    - <img src="https://render.githubusercontent.com/render/math?math=x_j \geq 0"> &nbsp;&nbsp;&nbsp; <img src="https://render.githubusercontent.com/render/math?math=(1 \leq j \leq n)">
* To get a more compact representation of linear programs, we use vectors and matrices.
* Let <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x}"> represent a (column) vector, <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x} = \langle x_1 \ldots x_n \rangle^T">.
* Define a partial ordering on the vectors in <img src="https://render.githubusercontent.com/render/math?math=\mathbb{R}^n"> by <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x} \leq \mathbf{y}"> if and only if the corresponding inequalities hold coordinate-wise, i.e. if and only if <img src="https://render.githubusercontent.com/render/math?math=x_j \leq y_j"> for all <img src="https://render.githubusercontent.com/render/math?math=1 \leq j \leq n">.
* Write the coefficients in the objective function as <img src="https://render.githubusercontent.com/render/math?math=\mathbf{c} = \langle c_1 \ldots c_n \rangle^T \in \mathbb{R}^n">, the coefficients in the constraints as an <img src="https://render.githubusercontent.com/render/math?math=m \times n"> matrix <img src="https://render.githubusercontent.com/render/math?math=A = (a_{ij})"> and the RHS values of the constraints as <img src="https://render.githubusercontent.com/render/math?math=\mathbf{b} = \langle b_1 \ldots b_m \rangle^T \in \mathbb{R}^m">.
* The standard form can be formulated simply as:
    - maximise <img src="https://render.githubusercontent.com/render/math?math=\mathbf{c}^T \mathbf{x}">
    - subject to the following two (matrix-vector) constraints:
        * <img src="https://render.githubusercontent.com/render/math?math=A \mathbf{x} \leq \mathbf{b}">
        * <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x} \geq \mathbf{0}">
* Thus, a Linear Programming optimisation problem can be specified as a triplet (<img src="https://render.githubusercontent.com/render/math?math=A, \mathbf{b}, \mathbf{c}">) which is the form accepted by most standard LP solvers.
* The full generality of LP problems does not appear to be handled by the standard form. LP problems could have:
    - equality constraints,
    - unconstrained variables (i.e. potentially negative values <img src="https://render.githubusercontent.com/render/math?math=x_i">), and
    - absolute value constraints.
* An **equality constraint** of the form <img src="https://render.githubusercontent.com/render/math?math=\sum_{i=1}^n a_{ij} x_i = b_i"> can be replaced by two inequalities <img src="https://render.githubusercontent.com/render/math?math=\sum_{i=1}^n a_{ij} x_i \geq b_i"> and <img src="https://render.githubusercontent.com/render/math?math=\sum_{i=1}^n a_{ij} x_i \leq b_i">. Thus, we can assume all constraints are inequalities.
* Each occurrence of an **unconstrained variable** <img src="https://render.githubusercontent.com/render/math?math=x_j"> can be replaced by the expression <img src="https://render.githubusercontent.com/render/math?math=x_j' - x_j^*"> where <img src="https://render.githubusercontent.com/render/math?math=x_j', x_j^*"> are new variables satisfying the equality <img src="https://render.githubusercontent.com/render/math?math=x_j' \geq 0, x_j^* \geq 0">.
* For a vector <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x} = \langle x_1, \ldots, x_n \rangle^T">, we can define <img src="https://render.githubusercontent.com/render/math?math=|\mathbf{x}| = \langle |x_1|, \ldots, |x_n| \rangle^T">. Some problems are naturally translated into constraints of the form <img src="https://render.githubusercontent.com/render/math?math=|A\mathbf{x}| \leq \mathbf{b}">. This also poses no problem as we can replace such **absolute value constraints** with two linear constraints: <img src="https://render.githubusercontent.com/render/math?math=A\mathbf{x} \leq \mathbf{b}"> and <img src="https://render.githubusercontent.com/render/math?math=-A\mathbf{x} \leq \mathbf{b}">.
* In the standard form, any vector <img src="https://render.githubusercontent.com/render/math?math=\mathbf{x}"> which satisfies the two constraints is called a **feasible solution**, regardless of what the corresponding objective value <img src="https://render.githubusercontent.com/render/math?math=\mathbf{c}^T \mathbf{x}"> might be.

#### Example

* **Maximise** <img src="https://render.githubusercontent.com/render/math?math=z(x_1, x_2, x_3) = 3x_1 %2B x_2 %2B 2x_3"> subject to:
    - <img src="https://render.githubusercontent.com/render/math?math=x_1 %2B x_2 %2B 3x_3 \leq 30">
    - <img src="https://render.githubusercontent.com/render/math?math=2x_1 %2B 2x_2 %2B 5x_3 \leq 24">
    - <img src="https://render.githubusercontent.com/render/math?math=4x_1 %2B x_2 %2B 2x_3 \leq 36">
    - <img src="https://render.githubusercontent.com/render/math?math=x_1, x_2, x_3 \geq 0">
* Adding the first two inequalities gives <img src="https://render.githubusercontent.com/render/math?math=3x_1 %2B 3x_2 %2B 8x_3 \leq 54">. Since all variables are constrained to be non-negative, then we know that <img src="https://render.githubusercontent.com/render/math?math=3x_1 %2B x_2 %2B 2x_3 \leq 3x_1 %2B 3x_2 %2B 8x_3 \leq 54">, i.e. the objective does not exceed 54. Can we do better?
* We try to look for coefficients <img src="https://render.githubusercontent.com/render/math?math=y_1, y_2, y_3 \geq 0"> to be used to form a linear combination of the constraints:
    - <img src="https://render.githubusercontent.com/render/math?math=y_1 (x_1 %2B x_2 %2B 3x_3) \leq 30y_1">
    - <img src="https://render.githubusercontent.com/render/math?math=y_2 (2x_1 %2B 2x_2 %2B 5x_3) \leq 24y_2">
    - <img src="https://render.githubusercontent.com/render/math?math=y_3 (4x_1 %2B x_2 %2B 2x_3) \leq 36y_3">
* Summing up all these inequalities and factoring, we get <img src="https://render.githubusercontent.com/render/math?math=x_1(y_1 %2B 2y_2 %2B 4y_3) %2B x_2(y_1 %2B 2y_2 %2B y_3) %2B x_3(3y_1 %2B 5y_2 %2B 2y_3) \leq 30y_1 %2B 24y_2 %2B 36y_3">.
* If we compare this to our objective, we see that if we choose <img src="https://render.githubusercontent.com/render/math?math=y_1, y_2, y_3"> such that:
    - <img src="https://render.githubusercontent.com/render/math?math=y_1 %2B 2y_2 %2B 4y_3 \geq 3">
    - <img src="https://render.githubusercontent.com/render/math?math=y_1 %2B 2y_2 %2B y_3 \geq 1">
    - <img src="https://render.githubusercontent.com/render/math?math=3y_1 %2B 5y_2 %2B 2y_3 \geq 2">
* then <img src="https://render.githubusercontent.com/render/math?math=3x_1 %2B x_2 %2B 2x_3 \leq x_1(y_1 %2B 2y_2 %2B 4y_3) %2B x_2(y_1 %2B 2y_2 %2B y_3) %2B x_3(3y_1 %2B 5y_2 %2B 2y_3)">.
* Combining this with the above inequalities, we get <img src="https://render.githubusercontent.com/render/math?math=30y_1 %2B 24y_2 %2B 36y_3 \geq 3x_1 %2B x_2 %2B 2x_3 = z(x_1, x_2, x_3)">.
* Consequently, in order to find a tight upper bound for our objective <img src="https://render.githubusercontent.com/render/math?math=z(x_1, x_2, x_3)"> in the original problem <img src="https://render.githubusercontent.com/render/math?math=P">, we have to find <img src="https://render.githubusercontent.com/render/math?math=y_1, y_2, y_3"> which solve problem <img src="https://render.githubusercontent.com/render/math?math=P^*">:
    - **Minimise** <img src="https://render.githubusercontent.com/render/math?math=z^* (y_1, y_2, y_3) = 30y_1 %2B 24y_2 %2B 36y_3"> subject to:
        * <img src="https://render.githubusercontent.com/render/math?math=y_1 %2B 2y_2 %2B 4y_3 \geq 3">
        * <img src="https://render.githubusercontent.com/render/math?math=y_1 %2B 2y_2 %2B y_3 \geq 1">
        * <img src="https://render.githubusercontent.com/render/math?math=3y_1 %2B 5y_2 %2B 2y_3 \geq 2">
        * <img src="https://render.githubusercontent.com/render/math?math=y_1, y_2, y_3 \geq 0">
* Then, <img src="https://render.githubusercontent.com/render/math?math=z^* (y_1, y_2, y_3) = 30y_1 %2B 24y_2 %2B 36y_3 \geq 3x_1 %2B x_2 %2B 2x_3 = z(x_1, x_2, x_3)"> will be a tight upper bound.
* This new problem <img src="https://render.githubusercontent.com/render/math?math=P^*"> is called the **dual problem** of <img src="https://render.githubusercontent.com/render/math?math=P">.
* We repeat the whole procedure to find the dual of <img src="https://render.githubusercontent.com/render/math?math=P^*">, denoted <img src="https://render.githubusercontent.com/render/math?math=(P^*)^*">. We are now looking for <img src="https://render.githubusercontent.com/render/math?math=z_1, z_2, z_3 \geq 0"> to obtain:
    - <img src="https://render.githubusercontent.com/render/math?math=z_1(y_1 %2B 2y_2 %2B 4y_3) \geq 3z_1">
    - <img src="https://render.githubusercontent.com/render/math?math=z_2(y_1 %2B 2y_2 %2B y_3) \geq z_2">
    - <img src="https://render.githubusercontent.com/render/math?math=z_3(3y_1 %2B 5y_2 %2B 2y_3) \geq 2z_3">
* Summing these up and factorising we get <img src="https://render.githubusercontent.com/render/math?math=y_1(z_1 %2B z_2 %2B 3z_3) %2B y_2(2z_1 %2B 2z_2 %2B 5z_3) %2B y_3(4z_1 %2B z_2 %2B 2z_3) \geq 3z_1 %2B z_2 %2B 2z_3">.
* If we choose multipliers <img src="https://render.githubusercontent.com/render/math?math=z_1, z_2, z_3"> such that:
    - <img src="https://render.githubusercontent.com/render/math?math=z_1 %2B z_3 %2B 3z_3 \leq 30">
    - <img src="https://render.githubusercontent.com/render/math?math=2z_1 %2B 2z_3 %2B 5z_3 \leq 24">
    - <img src="https://render.githubusercontent.com/render/math?math=4z_1 %2B z_3 %2B 2z_3 \leq 36">
* then <img src="https://render.githubusercontent.com/render/math?math=y_1(z_1 %2B z_2 %2B 3z_3) %2B y_2(2z_1 %2B 2z_2 %2B 5z_3) %2B y_3(4z_1 %2B z_2 %2B 2z_3) \leq 30y_1 %2B 24y_2 %2B 36y_3">.
* Combining this with the above we get <img src="https://render.githubusercontent.com/render/math?math=3z_1 %2B z_2 %2B 2z_3 \leq 30y_1 %2B 24y_2 %2B 36y_3">.
* Consequently, finding the double dual program <img src="https://render.githubusercontent.com/render/math?math=(P^*)^*"> amounts to **maximising** the objective <img src="https://render.githubusercontent.com/render/math?math=3z_1 %2B z_2 %2B 2z_3"> subject to the constraints:
    - <img src="https://render.githubusercontent.com/render/math?math=z_1 %2B z_2 %2B 3z_3 \leq 30">
    - <img src="https://render.githubusercontent.com/render/math?math=2z_1 %2B 2z_2 %2B 5z_3 \leq 24">
    - <img src="https://render.githubusercontent.com/render/math?math=4z_1 %2B z_2 %2B 2z_3 \leq 36">
* Thus, the double dual program <img src="https://render.githubusercontent.com/render/math?math=(P^*)^*"> is just <img src="https://render.githubusercontent.com/render/math?math=P"> itself.
* Recall that the **Ford-Fulkerson algorithm** produces a **maximum flow** by showing that it terminates only when we reach the capacity of a **minimal cut**. Looking for the multipliers <img src="https://render.githubusercontent.com/render/math?math=y_1, y_2, y_3"> reduced a maximisation problem to an equally hard minimisation problem.
* In general, the **primal** Linear Program <img src="https://render.githubusercontent.com/render/math?math=P"> and its **dual** <img src="https://render.githubusercontent.com/render/math?math=P^*"> are:

![linear-prog](images/linear-prog.png)
![linear-prog](images/linear-prog-1.png)

### Weak Duality Theorem

> If <img src="https://render.githubusercontent.com/render/math?math=x = \langle x_1 \ldots x_n \rangle"> is any feasible solution for <img src="https://render.githubusercontent.com/render/math?math=P"> and <img src="https://render.githubusercontent.com/render/math?math=y = \langle y_1 \ldots y_m \rangle"> is any feasible solution for <img src="https://render.githubusercontent.com/render/math?math=P^*">, then:
>
> <img src="https://render.githubusercontent.com/render/math?math=z(x) = \sum_{j=1}^n c_j x_j \leq \sum_{i=1}^m b_i y_i = z^*(y)"> **(proof omitted)**.

* Thus, the value of (the objective of <img src="https://render.githubusercontent.com/render/math?math=P^*"> for) any feasible solution of <img src="https://render.githubusercontent.com/render/math?math=P^*"> is an upper bound for the set of all values of (the objective of <img src="https://render.githubusercontent.com/render/math?math=P"> for) all feasible solutions of <img src="https://render.githubusercontent.com/render/math?math=P">, and every feasible solution of <img src="https://render.githubusercontent.com/render/math?math=P"> is a lower bound for the set of feasible solutions for <img src="https://render.githubusercontent.com/render/math?math=P^*">.
* If we find a feasible solution for <img src="https://render.githubusercontent.com/render/math?math=P"> which is equal to a feasible solution to <img src="https://render.githubusercontent.com/render/math?math=P^*">, this common value must be the **maximal feasible value** of the objective of <img src="https://render.githubusercontent.com/render/math?math=P"> and the **minimal feasible value** of the objective of <img src="https://render.githubusercontent.com/render/math?math=P^*">.

## Intractability

### Feasibility of Algorithms

* A (sequential) algorithm is said to be **polynomial time** if for every input it terminates in polynomially many steps in the length of the input.
* The **length of an input** is the *number of symbols* needed to describe the input precisely.

#### Decision Problems and Class <img src="https://render.githubusercontent.com/render/math?math=\mathbf{P}">

* A **decision problem** is a problem with a YES or NO answer.
* A decision problem <img src="https://render.githubusercontent.com/render/math?math=A(x)"> is in class <img src="https://render.githubusercontent.com/render/math?math=\mathbf{P}"> (*polynomial time*, denoted <img src="https://render.githubusercontent.com/render/math?math=A \in \mathbf{P}"> if there exists a polynomial time algorithm which solves it.

#### Class <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">

* A decision problem <img src="https://render.githubusercontent.com/render/math?math=A(x)"> is in class <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> (*non-deterministic polynomial time*, denoted <img src="https://render.githubusercontent.com/render/math?math=A \in \mathbf{NP}">) if there exists a problem <img src="https://render.githubusercontent.com/render/math?math=B(x,y)"> such that:
    1. for every input <img src="https://render.githubusercontent.com/render/math?math=x">, <img src="https://render.githubusercontent.com/render/math?math=A(x)"> is true if and only if there is some <img src="https://render.githubusercontent.com/render/math?math=y"> for which <img src="https://render.githubusercontent.com/render/math?math=B(x,y)"> is true, and
    2. the truth of <img src="https://render.githubusercontent.com/render/math?math=B(x,y)"> can be verified by an algorithm running in polynomial time in the length of <img src="https://render.githubusercontent.com/render/math?math=x"> only.
* We call <img src="https://render.githubusercontent.com/render/math?math=y"> a **certificate** for <img src="https://render.githubusercontent.com/render/math?math=x"> and <img src="https://render.githubusercontent.com/render/math?math=B"> a **certifier**.
* Class <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problems are problems that can be **verified in polynomial time** whereas Class <img src="https://render.githubusercontent.com/render/math?math=\mathbf{P}"> problems are problems that can be **solved in polynomial time**.
* For example, consider the decision problem <img src="https://render.githubusercontent.com/render/math?math=A(x) ="> "integer <img src="https://render.githubusercontent.com/render/math?math=x"> is not prime". Then we need to find a problem <img src="https://render.githubusercontent.com/render/math?math=B(x,y)"> such that <img src="https://render.githubusercontent.com/render/math?math=A(x)"> is true if and only if there is some <img src="https://render.githubusercontent.com/render/math?math=y"> for which <img src="https://render.githubusercontent.com/render/math?math=B(x,y)"> is true. Naturally, <img src="https://render.githubusercontent.com/render/math?math=B(x,y) ="> "<img src="https://render.githubusercontent.com/render/math?math=x"> is divisibe by <img src="https://render.githubusercontent.com/render/math?math=y">". <img src="https://render.githubusercontent.com/render/math?math=B(x,y)"> can indeed be verified by an algorithm running in polynomial time in the length of <img src="https://render.githubusercontent.com/render/math?math=x"> only.

#### <img src="https://render.githubusercontent.com/render/math?math=\mathbf{P}"> vs <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">

* Is it the case that *every* problem in <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> is also in <img src="https://render.githubusercontent.com/render/math?math=\mathbf{P}">?
* The conjecture that <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> is a strictly larger class of decision problems than <img src="https://render.githubusercontent.com/render/math?math=\mathbf{P}"> is known as the "<img src="https://render.githubusercontent.com/render/math?math=\mathbf{P} \neq \mathbf{NP}">" hypothesis, and it is widely considered to be one of the hardest open problems in mathematics.

### Polynomial Reductions

* Let <img src="https://render.githubusercontent.com/render/math?math=U"> and <img src="https://render.githubusercontent.com/render/math?math=V"> be two decision problems. We say that <img src="https://render.githubusercontent.com/render/math?math=U"> is **polynomially reducible** to <img src="https://render.githubusercontent.com/render/math?math=V"> if and only if there exists a function <img src="https://render.githubusercontent.com/render/math?math=f(x)"> such that:
    1. <img src="https://render.githubusercontent.com/render/math?math=f(x)"> maps instances of <img src="https://render.githubusercontent.com/render/math?math=U"> into instances of <img src="https://render.githubusercontent.com/render/math?math=V">.
    2. <img src="https://render.githubusercontent.com/render/math?math=f"> maps YES instances of <img src="https://render.githubusercontent.com/render/math?math=U"> to YES instances of <img src="https://render.githubusercontent.com/render/math?math=V"> and NO instances of <img src="https://render.githubusercontent.com/render/math?math=U"> to NO instances of <img src="https://render.githubusercontent.com/render/math?math=V">, i.e. <img src="https://render.githubusercontent.com/render/math?math=U(x)"> is YES if and only if <img src="https://render.githubusercontent.com/render/math?math=V(f(x))"> is YES.
    3. <img src="https://render.githubusercontent.com/render/math?math=f(x)"> is computable by a polynomial time algorithm.

#### Cook's Theorem

> Every <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problem is polynomially reducible to the SAT problem.

* **SAT problem:**

![sat-problem](images/sat-problem.png)

* There are <img src="https://render.githubusercontent.com/render/math?math=2^n"> cases to consider in the SAT problem.
* The SAT problem is in class <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> since given an evaluation of the propositional variables one can determine in polynomial time whether the formula is true for such an evaluation.
    - If each clause <img src="https://render.githubusercontent.com/render/math?math=C_i"> involves exactly two variables (**2SAT**), then we are in class <img src="https://render.githubusercontent.com/render/math?math=\mathbf{P}">.
* This means that for every <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> decision problem <img src="https://render.githubusercontent.com/render/math?math=U(x)"> there exists a polynomial time computable function <img src="https://render.githubusercontent.com/render/math?math=f(x)"> such that:
    1. for every instance <img src="https://render.githubusercontent.com/render/math?math=x"> of <img src="https://render.githubusercontent.com/render/math?math=U">, <img src="https://render.githubusercontent.com/render/math?math=f(x)"> produces a propositional formula <img src="https://render.githubusercontent.com/render/math?math=\Phi_x">;
    2. <img src="https://render.githubusercontent.com/render/math?math=U(x)"> is true if and only if <img src="https://render.githubusercontent.com/render/math?math=\Phi_x"> is satisfiable.

#### <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete

* An <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> decision problem <img src="https://render.githubusercontent.com/render/math?math=U"> is <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete (<img src="https://render.githubusercontent.com/render/math?math=U \in \mathbf{NP}">-<img src="https://render.githubusercontent.com/render/math?math=\mathbf{C}">) if every other <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problem is polynomially reducible to <img src="https://render.githubusercontent.com/render/math?math=U">.
* Thus, Cook's theorem says that SAT is <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete.
* <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete problems are the hardest <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problems since a polynomial time algorithm for solving an <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete problem would make every other <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problem also solvable in polynomial time.
* But if <img src="https://render.githubusercontent.com/render/math?math=\mathbf{P} \neq \mathbf{NP}"> (as commonly hypothesised), then there cannot be any polynomial time algorithms for solving an <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete problem.

#### Proving <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-completeness

> Let <img src="https://render.githubusercontent.com/render/math?math=U"> be an <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete problem, and let <img src="https://render.githubusercontent.com/render/math?math=V"> be another <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problem. If <img src="https://render.githubusercontent.com/render/math?math=U"> is polynomially reducible to <img src="https://render.githubusercontent.com/render/math?math=V">, then <img src="https://render.githubusercontent.com/render/math?math=V"> is also <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete **(proof omitted)**.

#### Reducing 3SAT to VC

* We want to find a polynomial time reduction from 3SAT to **Vertex Cover (VC)**.

![vertex-cover](images/vertex-cover.png)
![3sat-to-vc](images/3sat-to-vc.png)

* An instance of 3SAT consisting of <img src="https://render.githubusercontent.com/render/math?math=M"> clauses and <img src="https://render.githubusercontent.com/render/math?math=N"> propositional variables is satisfiable if and only if the corresponding graph has a vertex cover of size at most <img src="https://render.githubusercontent.com/render/math?math=2M %2B N"> **(proof omitted)**.

### Optimisation Problems

#### <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-hard Problems

* Let <img src="https://render.githubusercontent.com/render/math?math=A"> be a problem and suppose we have a "black box" device which for every input <img src="https://render.githubusercontent.com/render/math?math=x"> instantaneously computes <img src="https://render.githubusercontent.com/render/math?math=A(x)">.
* We consider algorithms which are *polynomial time in <img src="https://render.githubusercontent.com/render/math?math=A">*. This means algorithms which run in polynomial time in the length of the input and which, besides the usual computational steps, can also use the above mentioned "black box".
* We say that a problem <img src="https://render.githubusercontent.com/render/math?math=A"> is <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-hard (<img src="https://render.githubusercontent.com/render/math?math=A \in \mathbf{NP}">-<img src="https://render.githubusercontent.com/render/math?math=\mathbf{H}">) if every <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problem is polynomial time in <img src="https://render.githubusercontent.com/render/math?math=A">, i.e. if we can solve every <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problem <img src="https://render.githubusercontent.com/render/math?math=U"> using a polynomial time algorithm which can also use a black box to solve any instance of <img src="https://render.githubusercontent.com/render/math?math=A">.
* We do not require <img src="https://render.githubusercontent.com/render/math?math=A"> to be an <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}"> problem nor a decision problem. It can also be an optimisation problem.
* It is important to be able to figure out if a problem at hand is <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-hard in order to know that one has to abandon trying to come up with a feasible polynomial time solution.
* All <img src="https://render.githubusercontent.com/render/math?math=\mathbf{NP}">-complete problems are equally difficult because any of them is polynomially reducible to any other. However, the related **optimisation problems** can be very different. Some of these optimisation problems allow us to get within a constant factor of the optimal answer.
    - **Vertex Cover** permits an approximation which produces a cover at most twice as large as the minimum vertex cover.
    - **Metric TSP** permits an approximation which produces a tour at most twice as long as the shortest tour.
