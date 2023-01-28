# Big Oh Notation

# Asymptotic Growth Comparison

The following functions are from 'best' asymptotic growth to 'worst':

1. **Constant:** ﻿*f*(*n*)=*c*
2. **Logarithmic:** ﻿*f*(*x*)=log(*n*)
3. **Linear:** ﻿*f*(*n*)=*n*
4. **Linearithmic (n-log-n):** ﻿*f*(*n*)=*n*log(*n*)
5. **Quadratic:** ﻿*f*(*n*)=*n^*2
6. **Cubic:** ﻿*f*(*n*)=*n^*3
7. **Polynomials:** ﻿*f*(*n*)=*n^a*
8. **Factorial:** ﻿*f*(*n*)=*n*!
9. **Exponential:** ﻿*f*(*n*)=*a^n*
10. **Worst ever:** ﻿*f*(*n*)=*n^*

# Tricks

## **Gauss's sum identity:**

$$
\sum_{i=1}^ni=1+2+3+...+\left(n-1\right)+n=\frac{n\left(n+1\right)}{2}∑i=1ni=1+2+3+...+(n−1)+n=2n(n+1)
$$

## Geometric sum:

$$
∑a^i=1+a+a2+...+an=1−ra1(1−rm)
$$

-*m* is the number of terms, in this case *n*

-*a*1 is the first term, in this case 1

-*r* is the constant that each term is multiplied by to get the next term, in this case *a*

## Don't know the name

$$
1+2+...+2^{k-1}=2^k-11+2+...+2k−1=2k−1
$$

# Time complexity of recursive algorithm

There are multiple steps to this:

1. State / define the size of the input ﻿n
2. State the recurrence equation by counting operations. The exact amount of operations shouldn't be counted, that depends on the hardware, compiler and much more. So it is more about counting loops etc. Specific operations can be replaced by a constant, often called﻿ *cx* where ﻿*x* is a number
3. Create a form of this recurrence equation where there is ﻿*T*(*n*) in the equation anymore. There are 2 methods to do so:
    1. Making an educated guess and then proving this (by induction)
    2. Unfolding the equation and then create a final equation based on that
4. Determine the complexity in big O notation
5. Prove the complexity in big O notation

# [Complexity Analysis](https://www.notion.so/Algorithms-and-Data-Structures-fb37f2c092f245eb87deaeaec908ad6a)

Complexity Analysis boils down to analyzing the efficiency of an algorithm. This efficiency is measured by two elements:

- Time complexity - The amount of time it takes for a given algorithm to execute.
- Space complexity - The amount of space a given algorithm uses at most during execution.

### Empirical Time analysis

Empirical time analysis is an analysis method for time complexity that is roughly equivalent to a brute force approach when programming or a proof by exhaustion for Reasoning and Logic. You simply execute the algorithm and measure the time it takes to finish.

```java
long startTime = System.currentTimeMillis();// record the starting time
/* (run the algorithm) */
long endTime = System.currentTimeMillis();// record the ending time
long elapsed = endTime - startTime;// calculate the elapsed time
```

**Problems with empirical time analysis**

The most prominent problems with empirical time analysis are the following:

- Results may differ when different hardware / compiler / OS / etc. are used.
- Experiments are restricted to a limited set of inputs.
- Requires a full implementation of the algorithm.
- A compiler may optimize your code or require a warm up time.

## Theoretical complexity analysis for time

Theoretical complexity analysis for time is a way to analyse the efficiency of an algorithm without having to run additional code. In fact, you don't even need to execute your algorithm to analyse it.

What we do is, we assign a mathematical function to the algorithm that describes the running time.

$T_{algorithm}(n)=\text{"number of primitive operations performed for an input size n"}$

Number of primitive operations performed. What does this mean? Primitive operations are operations that have a run time of 1.

We consider the following primitive operations:

- Assigning a value to a variable
- Performing an arithmetic operation
- Comparing two numbers ( and no more than two)
- Accessing a single element of an array by index
- Calling and returning from a method

When setting up this  ﻿$T_{a\lg orithm}\left(n\right)$﻿ we go through a number of steps:

1. State the size of the problem *n* . Most often this is the length of  n
2. Simplify the program to only using primitive operations (optional).
3. Express the running time by counting operations.

*! Note that when expressing the running time, we consider the worst-case of our problem* ﻿n﻿ .

*! Note that a + only represents an arithmetic operation when applied to numbers.*

## Theoretical complexity analysis for space

Space complexity differs from time complexity in the sense that space used can go down, while time can not. You could say that space can be reused, while time is gone forever after it has been used. That's why we only look at the most space used at any given time during the execution of an algorithm when analyzing its space complexity. Where we counted the number of primitive operations performed for time complexity, for space complexity we count the number of stack frames used.

$S_{algorithm}(n)=\text{"maximum amount of memory needed at any point in the algorithm for an input size n"}$

To do this you have to remember that a stack frame is added or **pushed** onto the stack when a method is called and is only removed or **popped** off the stack when you return from the method. This means that with a recursive method, it is possible to have multiple stack frames on the stack at once.

## Big O proof

If we have a formula and a claimed Big O notation of that formula, we can prove whether this is the correct one. To prove this we first have to understand what it means for a Big O Notation to be correct. A Big O Notation $O\left(g\left(n\right)\right)O(g(n))﻿ ﻿O\left(g\left(x\right)\right)$﻿of a function ﻿$f\left(n\right)$﻿ is correct if there is a positive constant c such that    ﻿$f\left(n\right)\ \le\ c\ \cdot g\left(n\right)f(n) ≤ c ⋅g$ and there  is n such that n > n0