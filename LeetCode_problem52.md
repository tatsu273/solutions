## LeetCode Problems 52. N-Queens Ⅱ
## 問題
[問題](https://leetcode.com/problems/n-queens-ii/)
## 解法
```
class Solution:
    def totalNQueens(self, n: int) -> int:
        count = 0
        cols = set()
        diag1 = set()
        diag2 = set()
        def backtrack(row):
            if row == n:
                nonlocal count
                count += 1
                return
            for col in range(n):
                d1 = row + col
                d2 = row - col
                if col not in cols and d1 not in diag1 and d2 not in diag2:
                    cols.add(col)
                    diag1.add(d1)
                    diag2.add(d2)
                    backtrack(row+1)
                    cols.remove(col)
                    diag1.remove(d1)
                    diag2.remove(d2)
        backtrack(0)
        return count
```
