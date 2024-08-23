---
title:  COMP6466 Algorithm Notes
tags:
  - Algorithm
  - ANU COMP6466
  - Algorithm Analysis
  - Algorithm Design
  - Sort and Search
---

I will be highlighting the key points covered in the ANU COMP6466 Algorithm Course. 
This course aims to develop students' proficiency in algorithm analysis and design. 
The first five weeks focused on algorithm analysis, particularly deterministic and randomized algorithms, which I found very inspiring. 

These notes serve for me as a quick refresher of the course content, so I've omitted many mathematical notations.
## Week1

### Insertion Sort
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


### Useful But Forgettable Formulas
- $$\sum_{i=1}^{n}{i^2} = n*(n+1)(2n+1) / 6$$
- $$\sum_{i=1}^{n}{1+a+a^2+a^3+...+a^n} = (a^(n+1)-1 ) / (a-1)$$
- $$\sum_{i=1}^{n}{1^k+2^k+3^k+4^k+...+n^k} = (n^(k+1)) / (k+1)$$

### Asymptotic Notations

| Notations           | Equality                      |
|---------------------|-------------------------------|
| f(n) = O(g(n))      | 0 <= f(n) <= c*g(n)           |
| f(n) = o(g(n))      | 0 <= f(n) < c*g(n)            |
| f(n) = \W(g(n))     | 0 < c*g(n) <= f(n)            |
| f(n) = \w(g(n))     | 0 < c*g(n) < f(n)             |
| f(n) = \sigma(g(n)) | 0 < c1*g(n) <= f(n)<= c2*g(n) |

## Week2

### A question
So for all the f(n), will it satisfy f(n)=O(g(n)) or \sigma(g(n)) or \Omiga(g(n))?
No, e.g. f(n) = n, g(n) = n^(1+sin(n)).

### Time Complexity Order
1 < log(n) < n < nlog(n) = log(n!) < n^2 < n^3 < 2^n < n!

### Analysis


### Recurrence Analysis
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

## Week3
### Master Theorem



