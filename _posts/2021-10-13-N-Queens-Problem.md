---
layout: post
title:  N-Queens Problem
categories: [Backtracking, Hard Problem, Python]
---
 The N-Queen's problem is a classic example of backtracking, often implemented in the form of recursion. It is considered as a hard problem. The problem statement goes like this.
 > In a n x n board, locate n queens suct that no 2 queens can attack each other i.e. all queens should be in safe positions. Calculate the number of such solutions, for a value of n.


## What is Backtracking?
According to wikipedia, 
> Backtracking is a general algorithm for finding all(or some) solutions to some
> computational problems, which incrementally builds candidates to the solution and abandons a candidate("backtracks") as soon as it determines that the candidate cannot lead to a valid solution[^1].

The brute force solution would be to search across each board position and determine if it is safe to place a queen and continue till the last block. Such a solution would take O(N2N) time to get the result, which is far too slow.


[^1]: https://en.wikipedia.org/wiki/Backtracking
