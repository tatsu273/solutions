## LeetCode problem1504.Count Submetrics With All Ones

## 問題
[問題](https://leetcode.com/problems/count-submatrices-with-all-ones/description/)
## 解法
```
class Solution:
    def numSubmat(self, mat: List[List[int]]) -> int:
        ans = 0
        n, m = len(mat), len(mat[0])
        h = [0] * m
        ans = 0
        for i in range(n):
            for j in range(m):
                h[j] = h[j] + 1 if mat[i][j] else 0
            sumv, st = [0] * m, []
            for j in range(m):
                while st and h[st[-1]] >= h[j]:
                    st.pop()
                if st:
                    p = st[-1]
                    sumv[j] = sumv[p] + h[j] * (j - p)
                else:
                    sumv[j] = h[j] * (j + 1)
                st.append(j)
                ans += sumv[j]
        return ans
```
