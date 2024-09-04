---
title:  COMP6466 Algorithm Notes
tags:
  - Algorithm
  - ANU COMP6466
  - Algorithm Analysis
  - Algorithm Design
  - Sort and Search
---

I highlight the key points covered in the ANU COMP6466 Algorithm Course. 
This course aims to develop students' proficiency in algorithm analysis and design. 
The first five weeks focused on algorithm analysis, sort and search algorithm, particularly deterministic and randomized algorithms, which I found very inspiring. 

<!--more-->

<div class="page-views-container">
        <h6>Page Views</h6>
        <span id="page-views-today">Loading...</span>
        <span id="page-views">Loading...</span>
</div>
<br>

These notes serve as a quick refresher of the course content for me, so I've omitted many mathematical notations.

### Week1

#### Insertion Sort
Introduce the Insertion Sort, and its pseudocode is as follows, and the right side is the times the code executed: 
```
for j = 2 to A.length                   # (n-1)
    key = A[j]                          # (n-1)
    while i > 0 and A[i] > key:         # SUM(t_j) j from 2 to n
        A[i+1] = A[i]                   # SUM(t_j - 1) j from 2 to n
        i--                             # SUM(t_j - 1) j from 2 to n
    A[i] = key                          # (n-1)
```

Time Complexity Analysis:
$$c1(n-1) + c2(n-1) + c3 \sum_{j=2}^{n}{t_j}+c4 \sum_{j=2}^{n}{t_j-1}+c5(n-1)$$
$$ = c'n + c'' \sum_{j=2}^{n}{t_j}$$
$$ <= c'n + c'' \sum_{j=2}^{n}{j}$$
$$ = c'n + c'' (2+n) * (n-1) / 2$$
$$ = O(n^2)$$


#### Useful But Forgettable Formulas
- $$\sum_{i=1}^{n}{i^2} = n*(n+1)(2n+1) / 6$$
- $$\sum_{i=1}^{n}{1+a+a^2+a^3+...+a^n} = (a^(n+1)-1 ) / (a-1)$$
- $$\sum_{i=1}^{n}{1^k+2^k+3^k+4^k+...+n^k} = (n^(k+1)) / (k+1)$$

#### Asymptotic Notations

| Notations          | Equality                             |
|--------------------|--------------------------------------|
| f(n) = O(g(n))     | 0 <= f(n) <= c*g(n)                  |
| f(n) = o(g(n))     | 0 <= f(n) < c*g(n)                   |
| f(n) =  W(g(n))    | 0 < c*g(n) <= f(n)                   |
| f(n) =  w(g(n))    | 0 < c*g(n) < f(n)                    |
| f(n) = sigma(g(n)) | 0 < c1*g(n) <= f(n)<= c2*g(n)        |

### Week2

#### A question
So for all the f(n), will it satisfy f(n)=O(g(n)) or \sigma(g(n)) or \Omiga(g(n))?
No, e.g. f(n) = n, g(n) = n^(1+sin(n)).

#### Time Complexity Order
1 < log(n) < n < nlog(n) = log(n!) < n^2 < n^3 < 2^n < n!

#### Analysis


#### Recurrence Analysis
This part is one of the most important parts in this course. Three methods are introduced to help making recurrence Analysis:
1. Substitution Method
2. Recursion Tree
3. Master Theorem

The time cost of Recurrence Algorithms could always be written in this format: T(n) = a*T(n/b) + cf(n).

For the substitution method, we firstly make substitution for the T(n/k) and guess the law of T(n). 
Then we use Mathematical Induction to prove our guess.

For the Recursion Tree Method, draw the recursion tree, figure out the level, and the total time cost. Then guess what T(n)
looks like as well. Finally, using mathematical induction to prove our guess.

For the Master Theorem, remember all the formulas. Master Theorem is taught in week 3.

### Week3
#### Master Theorem
Consider T(n)=a*T(n/b)+f(n), a>=1, b>=1.
1. If 𝑓(𝑛) =𝑂(𝑛^{(log_𝑏^𝑎)−𝜖}) for some constant 𝜖>0,then  𝑇(𝑛) =Θ(𝑛^{log_𝑏^𝑎})
2. If 𝑓(𝑛) =Θ(𝑛^{log_𝑏^𝑎}) ,then  𝑇(𝑛) =Θ(𝑛^{log_𝑏^𝑎}log(n))
3. If 𝑓(𝑛) =\Omiga(𝑛^{(log_𝑏^𝑎)+𝜖}) for some constant 𝜖>0,and if 𝑎*𝑓(𝑛) ≤𝑐𝑓(𝑛) for some constant 𝑐<1 and 𝑛>𝑛0, then  𝑇(𝑛) =Θ(𝑛^{log_𝑏^𝑎}(log(n))^{k+1})


#### Search Problem
1. Binary Search O(log(n))
2. Two Sum Problem, do binary search for (v-a), time complexity: O(nlog(n))
3. The shortest sub-array Sum (slide window method)

#### Egg Dropping Problem
1. If we have unlimited number of eggs, using binary search method to drop egg (O(log(n))).
2. If we only have two eggs, using binary search + search from up to down.
3. More optimization: minimize the regret, d+(d-1)+(d-2)+(d-3)+...+1 = n. The worst case is O(sqrt(n)) < O(n).

#### Random Variable and Expectation
1. Coupon Problem
There are n kinds of coupons, how many coupons should we buy to collect n kinds of coupon.
Suppose X is the total number of trails. x_i is the trails to get the i-th type of coupon under the condition that we have i-1 types of coupons.

$$X = \Sum_{i=1}^{n}{x_i}$$

$$E[X] = E[\Sum_{i=1}^{n}{x_i}] = \Sum_{i=1}^{n}{E[x_i]}$$

When we have i-1 types of coupons, the probability that we get the i-th type coupon is:

$$P_i = 1-(i-1)/n = (n-i+1) / n$$

Therefore, E[x_i] = 1/ p_i = n / (n-i+1)
 
$$\Sum_{i=1}^{n}{E[x_i]} = \Sum_{i=1}^{n}{(n)/(n-i+1)} = n * \Sum_{i=1}^{n}{1/(n-i+1) = n* \Sum_{j=0}^{n-i}{1/(j+1)}} = n*log(n) + c*n$$

### Week4
#### The expectation of the inversion in Insertion Sort
In the Insertion Sort, the random step happens as we do the inversion of A[i] and A[j].
Suppose X is the total number of the inversion times. x_{i, j} = 1 is the event that A[i] and A[j] need inversion.

P_{i, j} = 1/2

E[x] = E[\Sum_{i=1}^{n}\Sum_{j=i+1}^{n}{x_{i, j}}] = \Sum_{i=1}^{n}\Sum_{j=i+1}^{n}{P_{i, j}}

=\Sum_{i=1}^{n}\Sum_{j=i+1}^{n}{1/2} = n*(n-1)/4

#### RandQuick Sort

The number of comparison between A[i] and A[j] is random. Let X be the number of comparison,
x_{i, j} = 1 be the event that A[i] and A[j] compare. for a sequence from i to j.
P_{i, j} = P(i as pivot) + P(j as pivot) = 1/ (j-i+1) + 1/(j-i+1) = 2/ (j-i+1)

Therefore, E[x] = E[\Sum_{i=1}^{n}\Sum_{j=i+1}^{n}{x_{i, j} = 1}] = E[\Sum_{i=1}^{n}\Sum_{j=i+1}^{n}{2/(j-i+1)}] =  2 * \Sum_{i=1}^{n}(log(n)+r) = 2nlog(n) + c


#### Randomized Algorithm

1. Verifying Matrix Multiplication

To verify the matrix multiplication A * B = C, we have basically deterministic algorithms, which takes O(n^3) and O(n^2.37) separately.
However, with randomized algorithm, we reduce the complexity to O(n^2).

Steps are:
- Generate an 𝑛 × 1 random 0/1 vector 𝑟.
- Compute𝑃=𝐴× 𝐵×𝑟 −𝐶𝑟
- Output Yes if 𝑃 is equal to zero vector and No otherwise.
- If 𝐴 × 𝐵 = 𝐶, then the algorithm always returns Yes.
- If 𝐴 × 𝐵 ≠ 𝐶, then the probability it returns Yes is at most 1⁄2 (not proved in this course).

Then we can repeat the original algorithm _k_ times. If all the outputs are Yes, then return Yes, otherwise return No.
The probability it returns Yes while the answer is actually No is atmost 1 / 2^_k_.

The time complexity of this randomized algorithm is O(k*n^2) = O(n^2).

### Week5

#### In place and Stable
Two important concepts of sorting algorithm is in place and stable.

**In place** means the arrangement happens inside the array; does not need additional memory.

**Stable** means elements with the same values appear in the output array in the same order as they appear in the input array.

| Sort Methods-> | Insertion Sort | Merge Sort | RandQuick Sort | Count Sort | Bucket Sort | Radix Sort |
|----------------|----------------|------------|----------------|------------|-------------|------------|
| In place       | Yes            | No         | Yes            | No         | No          | No         |
| Stable         | Yes            | Yes        | No             | Yes        | Yes         | Yes        |

Bucket Sort use Insertion Sort inside its lists, therefore it's stable;

Radix Sort uses Count Sort when comparing the same digit, therefore not in place but stable.

#### The complexity
Count Sort: O(N+M)

Bucket Sort: Average Complexity O(n)

Radix Sort: Average Complexity O(d*n)


#### Divide-and-Conquer Problem

O(nlog(n))


<body data-article-id="post-algorithm-notes">

</body>

<div class="like-button-container">
    <button id="like-button" onclick="incrementLike()">👍 Like</button>
    <span id="like-count">Loading...</span>
</div>