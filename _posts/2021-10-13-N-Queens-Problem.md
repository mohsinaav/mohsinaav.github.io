---
layout: post
title:  N-Queens Problem
categories: [Backtracking, Hard Problem, Python]
---
 The N-Queen's problem is a classic example of backtracking, often implemented in the form of recursion. It is considered as a hard problem. The problem statement goes like this.
 > In a n x n board, locate n queens suct that no 2 queens can attack each other i.e. all queens should be in safe positions. Calculate the number of such solutions, for a value of n.


## What is Backtracking?
According to wikipedia, 
> [Backtracking](https://en.wikipedia.org/wiki/Backtracking) is a general algorithm for finding all(or some) solutions to some
> computational problems, which incrementally builds candidates to the solution and abandons a candidate("backtracks") as soon as it determines that the candidate cannot lead to a valid solution.

The `brute force` solution would be to search across each board position and determine if it is safe to place a queen or not and continue till the last block. Such a solution would take $O(N^2)$ time to get the result, which is far too slow.

Here I am going to explain the backtracking solution. The key points to keep in mind are:
<ol type="a">
 <li><strong>We can consider a board as a 2-dimensional list with all entries as 0. Placing a queen means 0 turns 1.</strong> During backtracking, removing a queen means 1 turns  back to 0. Todo: add a picture here.</li>
 
 <li>If a queen is placed in a row, no more queen can be placed in that particular row. So move on to the next row. </li><br> 
 <i>We will keep track of the columns that already has a queen in it.</i>
 
 <li>Each position on the baord, has its diagonal values, calculated as $ diag = row + col $ <br>
  If we determine these diagonal values, the board would look like this: 
    Todo: add a diagonal pic here.</li><br>
 
  For example, if a queen is placed at pos (1,1), then its diagonal value is 2.  Other positions like (2,0) and (0,2) have same diagonal values and thus are not safe for any other queens. *We will be keeping track of these diag values at each position, whenever a queen is added.*
 
 <li>Similarly, anti-diagonal values are calculated as $ anti-diag = row - col $<br>
  The anti-diagonal values of each position on the board would look like this:
  Todo:add a anti-diagonal pic here.</li><br> 
 <i>Again, we will be keeping track of anti-diagonal values.</i><br>
 
 <li>At any current position, we can determine if it is under attack by any of the previous queens, by validating if the current position is already present in any of the three above lists, mentioned in points b,c and d. </li>
</ol>


### Psuedo code:
1. Create a board - list(list(n)) n x n elements, all values 0
2. Utility function to display the board later.
3. Define a recursive function that takes in multiple arguments:  
     - n: number of row or column in the board, 
     - row: current row value, 
     - count: to keep track of column value, 
     - cols: set of columns of queens already placed, 
     - diags: set of diagonal values and 
     - anti_diags: set of anti-diagonal values.
4. Go through each column one by one, starting from 0, till n.
5. Determine the current diagonal and ant-diagonal value
6. Check If current row is already in cols set, or current diag value is in diag set or current anti-diag value is in anti-diag set.
7. If present, skip to the next column.
8. Else, place a queen at this location by changing 0 to 1.
9. Add current values to respective sets.
10. Next call the recursive function for the next row until we reach the last row.
11. If it is the last row, increment the count value and return it.
12. Once the count value is returned, remove the last added values from different sets added before. This is the back tracking step.

Finally, we will get the count of possible solution.

### Python solution:
```
class Solution(object):
  def __init__(self):
    self.board = [[]]
    
  def set_board(self, n):
    self.board = [[0] * n for _ in range(n)]
    
  def display_board(self, n):
    i = 0
    for i in range(n):
      print(f"{self.board[i]}")
      
  def backtrack_N_Queens(self, n, row, count, cols, diags, anti_diags):
    for col in range(n):
      cur_diag = row + col
      cur_antidiag = row - col
      
      if (col in cols or cur_diag in diags or cur_antidiag in anti_diags):
        continue
       
      self.board[row][col] = 1
      cols.add(col)
      diags.add(cur_diag)
      anti_diags.add(cur_antidiag)
      
      if row == n-1:
        count += 1
      else:
        count = self.backtrack_N_Queens(n, row + 1, count, cols, diags, anti_diags)
        
      anti_diags.remove(cur_antidiag)
      diags.remove(cur_diag)
      cols.remove(col)
      self.board[row][col] = 0
    
    return count
  
  if __name__ == "__main__":
    sol = Solution()
    n = int(input("Enter the value of n: "))
    sol.set_board(n)
    res = sol.backtrack_N_Queens(n, row = 0, count = 0, cols = set(), diags = set(), anti_diags = set())
    print(f"Number of available solutions  for a {n} x {n} board are ",res)      
  
```

I am pretty sure, there must be various ways to implement the backpropagation solutions for this problem. 
Todo: Add time and space complexity for brute force and back tracking.

