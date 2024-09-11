---
title:  ANU High Performance Computing Notes
tags:
  - High Performance Computing
  - HPC
  - ANU COMP6464
---

The learning notes of ANU COMP6464 High Performance Scientific Computation.
For learning(beginners), recapping, exams preparation.

<!--more-->

<div class="page-views-container">
        <h6>Page Views</h6>
        <span id="page-views-today">Loading...</span>
        <span id="page-views">Loading...</span>
</div>
<br>

#### Outline
1. Week 1 - Course Introduction and Von Neumann Architecture Measuring Performance
2. Week 2 - Computing with Real Numbers
3. Week 3 - CPU and Memory Architecture
4. Week 4 - Mid-Semester Test
5. Week 5 - Scalar Profiling and Compiler Optimisations
6. Week 6 - Data Access Optimisations

### Week 5

#### Compiler Auto-vectorization
Compiler auto-vectorization is one of the methods to make SIMD operations.

Using -O3 to enable vectorization in GCC.

It's easy to think about converting loops into vectorized operations. However, not all kinds of loops are good candidate 
for auto-vectorization. The property of good loops:
1. countable.
2. No break.
3. No branch.
4. No function call.
5. No aliasing.
6. No data dependencies(RAW, WAW, WAR).

So right now, we may know some tips to improve auto-vectorization. (Try to make the loop become a good loop.)

If the loops carry dependency or function calls

##### Example 1 SAXPY

Compiling the code using vectorization options:
**gcc -c -O3 -fopt-info-vec-all saxpy.c**

##### XMM YMM ZMM
- XMM (128-bit): used for processing floating point or small vectors, belongs to SSE instruction set.
- YMM (256-bit): Used for processing larger vector data, belonging to the AVX instruction set.
- ZMM (512-bit): Provides the highest level of parallelism for handling larger-scale data, belonging to the AVX-512 instruction set.

##### Useful GCC flags 
These are some gcc optimization flags that we need to remember:

- -O3: Enables advanced optimizations to improve performance.
- -mavx2: Enables the AVX2 instruction set, using 256-bit vector registers to accelerate computations.
- -mavx512f: Enables the AVX-512 instruction set, using 512-bit registers for even higher parallelism.
- -mprefer-vector-width=512: Prefers 512-bit vector width when vectorizing, combined with AVX-512 for performance boosts.
- -funsafe-math-optimizations: Enables unsafe math optimizations, potentially boosting performance but at the cost of some accuracy.

#### Compiler Intrinsic Functions
Compiler intrinsic functions provide a method to directly call compiler instructions. However, using compiler intrinsic 
is not portable. Therefore, conditional compiling must be used to make sure the program can run on computing systems 
with different instruction set.

![Version1](https://github.com/TommyGong08/tommygong08.github.io/blob/main/_posts/figs/0909/5-1.jpg?raw=true)

#### Intel Intrinsic Guide
If you forget the names of intel intrinsic guide functions, refer to:
 https://www.intel.com/content/www/us/en/docs/intrinsics-guide/index.html


#### Optimizing SAXPY By Intrinsic Functions
Know how to use _mm256_loadu_ps, _mm256_fmadd_ps, _mm256_mul_ps, _mm256_add_ps to realize Parallelized SAXPY.

Remember two methods to optimze SAXPY(Single-precision A X Plus Y):
1. AVX
2. FMA

FMA uses _mm256_fmadd_ps, integrating both _mm256_mul_ps and _mm256_add_ps.

**Further optimization**: Combining Loop unrolling and FMA/AVX, you could get higher FLOPS and Less Cycles.
<br>

### Week 6
This week’s lecture mainly talks about data access optimizations. Two examples, the matrix transpose and matrix multiply
are given to show how to optimize data access.

#### Matrix Transpose
The operations to generally optimize matrix transpose:
- Flipping
- Loop Unrolling and Jam
- Blocking Algorithms

Comparing the following two Matrix Transpose version;

Version 1:

![Version1](https://github.com/TommyGong08/tommygong08.github.io/blob/main/_posts/figs/0909/1.jpg?raw=true)

Version 2:

![Version2](https://github.com/TommyGong08/tommygong08.github.io/blob/main/_posts/figs/0909/2.jpg?raw=true)

In version 1, Reads are stride 1, and Writes are stride N.
When we analyse the overall performance of these code, N and Cache Write policy should be taken into account.
For a small N, we don't need to consider the cache read miss and write miss. But for a large N, analysing the cache status is quite important.

Since writes miss is more expensive than reads miss both in write-through or write-back policy, flipping  may improve the performance. 
The overall performance of version 2 better than version 1, as the Reads are stride N, and Writes are stride 1.

Version 3: Loop Unrolling + Flipping

![Version3](https://github.com/TommyGong08/tommygong08.github.io/blob/main/_posts/figs/0909/3.jpg?raw=true)

Less cache misses per iteration by loop unrolling.

Version 4: Blocking Algorithm of Matrix Transpose.
Separating the matrix into several blocks, then do matrix transpose in each block.
Why? Try to better use L1/L2 cache, aim to maximize the cache use efficiency.


#### Matrix Multiply
The slide introduces three methods to improve the performance.
- Transpose
- Flipping
- Blocking

The original code for Matrix Multiply is :

![Original](https://github.com/TommyGong08/tommygong08.github.io/blob/main/_posts/figs/0909/4.jpg?raw=true)

The time complexity of the original method is O(N^3).
The cache miss situation for this code is:
1. Reads from A with stride 1
2. Reads from B with stride N
3. Writes to C with stride N

Then we may do outer loop flipping:

![Image5](https://github.com/TommyGong08/tommygong08.github.io/blob/main/_posts/figs/0909/5.jpg?raw=true)

The cache miss situation for this code is:
1. Reads from A with stride 1
2. Reads from B with stride N
3. Writes to C with stride 1

Though make outer loop flipping, we may find the GFlops essentially the same. Because both these two code always need to
 use L2 cache. L1 cache is not enough.

Next, transpose matrix B:

![Image6](https://github.com/TommyGong08/tommygong08.github.io/blob/main/_posts/figs/0909/6.jpg?raw=true)

After generate Matrix D by transposing Matrix B, we could make the inner loop with:
1. Reads from A with stride 1
2. Reads from D with stride 1
3. Writes to C with stride 1
The time complexity of Transpose Matrix B is O(N^2).

Next, try to make further optimization. We can flip the k loop.

![Image7](https://github.com/TommyGong08/tommygong08.github.io/blob/main/_posts/figs/0909/7.jpg?raw=true)

1. Reads from A constant
2. Reads from D with stride 1
3. Writes to C with stride 1

This flipping k loop operation could result in significant improvement in GFlops.

Last but not least, the blocking algorithm is one of the optimization methods. However, we need to pay attention to the 
balance between block size and cache miss rate. From the results of the experience, a block size of 8 gives better 
performance.

#### Summary
Once we want to do data access optimization, think about the following methods:
1. Flipping
2. Loop unrolling and jam
3. Make blocked version
4. (Try) Efficient implementation using AVX instructions

Remember, the cache write miss is more expensive than cache read miss. 
The fewer cache misses, the better the code. The less memory access, the better the code.




(Continuous updates ... )


<body data-article-id="post-comp6464-HPC-notes">
</body>

<div class="like-button-container">
    <button id="like-button" onclick="incrementLike()">👍 Like</button>
    <span id="like-count">Loading...</span>
</div>