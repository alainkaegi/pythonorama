# Analysis of Algorithms
## Timing
You often want to know how *efficient* an algorithm is, usually in terms of time. This can help answer questions such as:
- Which of these two algorithms is faster?
- Is this algorithm fast enough for your purposes?

For a gross estimate (or empirical verification), you can implement an algorithm and time it, using a stopwatch or using code like this:
```python
import time
before = time.time()
# run the algorithm to be timed
print(str(time.time() - before) + ' sec elapsed')
```
(The function `time.time` returns the number of seconds since [the beginning of 1970](https://en.wikipedia.org/wiki/Unix_time).)

There are a number of problems with this approach:
- The result may be affected by the programming language used, the speed of the physical machine, or other processes running on that machine. The last issue can be ameliorated by shutting down other programs such as web browsers, but a modern system often has dozens of processes running even when there are no other user programs running.
- Implementing an algorithm is difficult and time-consuming. You would prefer to know the result beforehand.
- The result is likely to depend on the size of the input. For example, it takes longer to sort a million numbers than ten.
- The result may depend on the specific input. For example, some algorithms take longer to sort a list of numbers that is currently in reverse order than a list in random order.

For these reasons, you turn to mathematical analysis tools such as asymptotic notation.

## Asymptotic Notation
### Running Time Functions
You can express the time taken by an algorithm as a function, such as $3n^2 + 2$, where $n$ is the size of the input. Running an algorithm on larger inputs generally takes more time.

In most cases it will be clear from context what $n$ means: the length of the array being sorted, the number of items stored in the data structure, etc. Running time functions usually take only one argument, but there are exceptions. Significantly, you express the running time for a graph algorithm in terms of $v$ (the number of vertices in the graph) and $e$ (the number of edges in the graph).

### Orders
Given the running time functions for two algorithms, which algorithm is faster? This question appears to open a can of mathematical worms, but there is a huge shortcut: asymptotic notation. This concerns what happens as $n$ becomes large.

Functions can be grouped into orders. An order is a set of functions. For example, $\Theta(n^2)$, pronounced "big theta of $n^2$" or "order $n^2$," is the set of functions that grow about like $n^2$. This set includes functions such as $n^2$, $3n^2 + 2$, and $5n^2 + 2n + 12$.

The table below summarizes the most commonly occurring orders.

Order             | Nickname
-|-
$\Theta(2^n)$     | exponential
$\Theta(n^3)$     | cubic
$\Theta(n^2)$     | quadratic
$\Theta(n\log n)$ | linearithmic
$\Theta(n)$       | linear
$\Theta(\log n)$  | logarithmic
$\Theta(1)$       | constant

Orders are useful for two reasons:
- It is often relatively easy to tell which order a function is in.
- That is often enough information to tell which one grows more quickly.

To tell what order a function is in, you take advantage of two rules:
1. Adding or subtracting a term from a lower order doesn't matter.
1. Multiplying by a positive constant factor doesn't matter.

For example, the first rule tells us that $5n^2 + 2n + 12$ is in the same order as $5n^2$, because the lower-order terms $2n$ and $12$ don't matter. When $n$ is large, these terms are vanishingly small compared to $5n^2$.

The second rule tells us that $5n^2$ is in $\Theta(n^2)$, because the constant factor $5$ doesn't matter. Ignoring the constant factor means that your analysis doesn't depend on details like the speed of the hardware; if an algorithm takes time in $\Theta(n^2)$, that won't change if you run it on a machine that is twice as fast.

If you know what orders two functions are in, it's easy to compare them. For example, suppose:


$f(n) \in \Theta(n^2)$  
$g(n) \in \Theta(n^3)$

Clearly, $g(n)$ is larger for large $n$. You would therefore prefer an algorithm whose running time is $f(n)$, because it takes less time on large inputs.

### Related Notations
There are several related asymptotic notations referring to unions of multiple orders. For example, the set $O(n)$, pronounced "big O of $n$," is the union of $\Theta(n)$ and all lower orders. If you say that a function is in $O(n)$, you mean that it is in $\Theta(n)$ or some lower order.

The related notations are summarized in the table below. Phrasing such as "much more" or "about like" is meant to emphasize that there is a constant factor of "wiggle room" within a given order.

Notation | Pronounced | Idea | Combines | $f$ Grows
-|-|-|-|-
$f \in \Omega(g)$ | $f$ is in big omega of $g$ | $\Theta(f) \geq \Theta(g)$ | $\Theta(g)$ and higher orders | like $g$ or much more quickly
$f \in \Theta(g)$ | $f$ is in big theta of $g$ | $\Theta(f) = \Theta(g)$ | $\Theta(g)$ | about like $g$
$f \in O(g)$ | $f$ is in big o of $g$ | $\Theta(f) \leq \Theta(g)$ | $\Theta(g)$ and lower orders | like $g$ or much more slowly

## Analyzing Algorithms
### Non-Recursive Algorithms
Any operation whose time doesn't depend on the size of its input takes constant time. This includes assignments and arithmetic operations on primitive numbers (which are of bounded size).

To analyze a non-recursive algorithm, ask of each step:
- How long does this step take?
- How many times is this step executed?

Multiplying these two values gives the total time cost of that step. The time for the entire algorithm is the sum of these costs.

For example, consider this function:
```python
def sum(n):
    sum = 0
    i = 1
    while i <= n:
        sum += i
        i += 1
    return sum
```
Analyzing this line-by-line, you assign a lettered constant for the amount of time taken by each step. You don't know exactly how long each step takes and, because you only need to know the order of the result, you don't care.

Line            | Cost | Times   | Total
-|-|-|-
`sum = 0`       | $a$  | $1$     | $a$
`i = 1`         | $b$  | $1$     | $b$
`while i <= n:` | $c$  | $n + 1$ | $cn + c$
`sum += i`      | $d$  | $n$     | $dn$
`i += 1`        | $e$  | $n$     | $en$
`return sum`    | $f$  | $1$     | $f$

This adds up to:

$a + b + cn + c + dn + en + f$

Since lower order terms don't matter, this in the same order as

$cn + dn + en = (c + d + e)n$

which is in $\Theta(n)$.

This technique works, but with practice you can often simply find the step that runs most frequently. All other steps are in the same order or lower orders, so they don't matter.

One subtlety to watch out for: one line of code may involve multiple steps, especially if it includes a method call.

### Best-Case, Average, Worst-Case, and Amortized Analysis
Consider this function:
```python
def linear_search(key, array):
    for i in range(len(array)):
        if array[i] == key:
            return True
    return False
```
The number of times the loop runs depends not just on $n$ (the length of the array `array`) but also on the *contents* of `array`. In a situation like this, you must clarify whether a statement is about best-case, average, or worst-case performance.

Suppose `key` is present in `array` at exactly one place. In the best case, `key` is at index 0, so the loop only runs once. You can say that this algorithm takes constant time in the best case.

In the worst case, `key` is in the last position (index $n - 1$), so the algorithm takes linear time.

Average case analysis can be a bit trickier, because you have to make additional assumptions about how likely various possibilities are. For this algorithm, let's assume that `key` is equally likely to be at any position in the array. The average number of passes through the loop is therefore:

$\frac{1}{n}\sum_{i = 1}^n{i} = \frac{n + 1}{2} \in \Theta(n)$

The best-case running time of an algorithm is always at least as good as its average running time, which in turn is at least as good as its worst-case running time.

On some occasions you will do amortized analysis, which asks, "What's the average behavior over the worst possible sequence of operations?" For almost all algorithms, this is exactly the same as worst-case analysis, because the worst possible sequence of operations is just the worst individual operation over and over again. For some data structures (notably resizable arrays) the worst operation *can't* happen over and over again, so the amortized result may be better. Amortized running time is always at least as good as worst-case and at least as bad as average.

In summary:

Analysis | Question Answered
-|-
Worst-case | How long will this take for the worst individual operation?
Amortized | How long will this take per operation for the worst sequence of operations?
Average | How long will this take per operation over a typical sequence of operations?
Best-case | How long will this take for the best individual operation?

### Recursive Algorithms
Here is a recursive algorithm for summing the numbers in an array, implemented as two functions:
```python
def sum(array):
    return _sum(array, 0)

def _sum(array, i):
    if i == len(array) - 1:
        return a[i]
    return a[i] + _sum(array, i + 1)
```
What is the order of its running time? The non-recursive method does nothing but call the other one and return the result, so it is the second method you must examine. Your normal technique doesn't work because it's not clear how long the recursive call takes.

To analyze a recursive algorithm, you first write a special equation called a recurrence relation. For this algorithm, the recurrence relation is:

$T(n)=\begin{cases}1 \textrm{ if } n = 1 \\\\ 1 + T(n - 1)\textrm{ otherwise }\end{cases}$

The upper part says that the time to process $n$ numbers is constant in the base case where $n = 1$. It won't matter what the constant is, so you choose $1$ for simplicity.

The lower part says that, in the recursive case, the time is a constant plus the time to process $n - 1$ elements.

To get to an order, you need to solve the recurrence relation, that is, find an equivalent closed form equation that doesn't have $T(n)$ on the right side. In this case the solution is:

$T(n) = n$

This can be verified by substituting the solution into the recurrence relation.

Solving recurrence relations is an advanced topic, but fortunately a few specific cases cover most of the recursive algorithms you'll encounter. They are summarized in the table below, which omits the base case lines as they don't affect the order of the solutions.

Recurrence Relation | Solution Order
-|-
$T(n) = n + T(n - 1)$  | $\Theta(n^2)$
$T(n) = n + 2T(n/2)$   | $\Theta(n \log n)$
$T(n) = 1 + T(n - 1)$  | $\Theta(n)$
$T(n) = n + T(n/2)$    | $\Theta(n)$
$T(n) = 1 + T(n/2)$    | $\Theta(\log n)$

## Resources
- Short [video lecture](https://www.youtube.com/watch?v=w7-6h64HSQ8) on asymptotic notation
- OpenDSA, [Algorithm Analysis](https://opendsa-server.cs.vt.edu/ODSA/Books/Everything/html/AnalChap.html)
- Sedgewick, Wayne, and Dondero, *Introduction to Programming in Python*, [Section 4.1](https://introcs.cs.princeton.edu/python/41analysis/)
- Sedgewick and Wayne, *Introduction to Programming in Java*, [Section 4.1](https://introcs.cs.princeton.edu/java/41analysis/)
- Sedgewick and Wayne, *Algorithms, 4th Edition*, [Section 1.4](https://algs4.cs.princeton.edu/14analysis/)
- Cormen *et al.*, *Introduction to Algorithms, 3rd Edition*, Chapters 3-4
- [Big-O Emoji](https://devrant.com/rants/1858258/big-o-emoji)

## Questions
1. :star: What is the order of the solution to the recurrence relation $T(n) = n + 2T(n/2)$?
1. :star::star: What's wrong with the following statement?
   > Since $n^3$ grows more quickly than $n^2$, an algorithm with cubic running time is faster than one with quadratic running time.
1. :star::star: Suppose you know that $f(n) \in O(n^2)$, $g(n) \in O(n^3)$, and $h(n) \in \Omega(n^3)$.
   1. What can you conclude about the relationship between $\Theta(f(n))$ and $\Theta(g(n))$?
   1. What can you conclude about the relationship between $\Theta(f(n))$ and $\Theta(h(n))$?
   1. What can you conclude about the relationship between $\Theta(g(n))$ and $\Theta(h(n))$?
1. :star::star: Suppose you know that $f(n) \in O(g(n))$. Can you conclude that $f(n) \leq g(n)$ for small values of $n$? What about for large values?
1. :star::star: What is the order of the running time of the `linearSearch` algorithm above when `key` is not present in `a`?
1. :star::star: What's wrong with the following statement?
   > The best case for the algorithm I'm analyzing occurs when $n = 1$.
1. :star::star: What is the order of the worst-case running time of the method below?
    ```python
    def mystery(arr, k):
        lo = 0
        hi = len(arr)
        while lo < hi:
            if arr[lo] == k:
                return True
            lo += 1
        return False
    ```
1. :star::star: What is the order of the running time of the code below?
    ```python
    for i in range(n):
        for j in range(n):
            print(str(i) + ', ' + str(j))
    ```
1. :star::star: What is the order of the running time of the code below?
    ```python
    i = n
    while i > 0:
        print(str(n))
        i //= 2
    ```
1. :star::star::star: What statement in asymptotic notation is equivalent to the following?
   > There exists some $c > 0$ and some $n_0$ such that, for all $n \geq n_0$, $f(n) \leq cg(n)$.
1. :star::star::star: Read the definition of the $\sim$ notation on the Sedgewick, Wayne, and Dondero, [Section 4.1](https://introcs.cs.princeton.edu/python/41analysis/). Given two functions $f(n)$ and $g(n)$, what is the relationship between the statements $f(n) \sim g(n)$ and $f(n) \in \Theta(g(n))$? In other words, does one statement imply the other, vice versa, neither, or both?
1. :star::star::star: The notation $f \in O(g)$ means that $f$ is either in the same order as $g$ or a lower order. Is there a notation that means $f$ is in a strictly lower order?

## Answers
1. $\Theta(n \log n)$
1. If the running time grows quickly, then it is very large for large values of $n$. To have a large running time is to be slow.
1.
   1. Nothing.
   1. $\Theta(f(n))$ is a lower order than $\Theta(h(n))$.
   1. Either $\Theta(g(n))$ is a lower order than $\Theta(h(n))$ or they are both the same order, namely $\Theta(n^3)$.
1. No. Asymptotic notation says nothing about small values of $n$. For large values, you know that $f(n)$ exceeds $g(n)$ by no more than a constant factor, but it might be that $f(n) = 10n$ and $g(n) = n$.
1. Linear.
1. Best-case, average, amortized, and worst-case analysis must apply for all values of $n$. If they differ, they must do so between different inputs of each size. For example, a sorting algorithm might have a best case when the array is already sorted and a worst case when it is already sorted in reverse order.
1. $\Theta(n)$. In the worst case, the loop examines each of the $n$ elements of `arr`.
1. $\Theta(n^2)$. The innermost line takes constant time. The inner loop runs $n$ times each time the outer loop runs. The outer loop runs $n$ times, so the innermost line runs a total of $n^2$ times.
1. $\Theta(\log n)$
1. $f(n) \in O(g(n))$
1. $f(n) \sim g(n)$ implies $f(n) \in \Theta(g(n))$, but not vice versa. For example, if $f(n) = n$ and $g(n) = 2n$, then $f(n) \in \Theta(g(n))$ but it is not true that $f(n) \sim g(n)$. The $\sim$ notation ignores lower-order terms just like $\Theta$ notation does, but it does not ignore constant factors.
1. Yes: $f \in o(g)$. Similarly, $f \in \omega(g)$, where $\omega$ is a lower-case omega, means that $f$ is in a strictly higher order.
