## LeetCode problems 1320. Minimum Distance to Type a Word Using Two Fingers
1. MultidimentionalDP
```
class Solution:
    def minimumDistance(self, word: str) -> int:
        def getDistance(A, B):
            Ax, Ay = divmod(A, 6)
            Bx, By = divmod(B, 6)
            return abs(Ax-Bx) + abs(Ay-By)

        dp = [[[float("inf")] * 26 for j in range(26)] for i in range(len(word)+1)]
        for j in range(26):
            for k in range(26):
                dp[0][j][k] = 0
        for i in range(len(word)):
            idx = ord(word[i])-ord("A")
            for j in range(26):
                for k in range(26):
                    dp[i+1][idx][k] = min(dp[i+1][idx][k], dp[i][j][k] + getDistance(idx, j))
                    dp[i+1][j][idx] = min(dp[i+1][j][idx], dp[i][j][k] + getDistance(idx, k))
                    
        ans = float("inf")
        for j in range(26):
            for k in range(26):
                ans = min(ans, dp[-1][j][k])
        return ans        
```

2. DP
```
class Solution:
    def minimumDistance(self, word: str) -> int:
        def get_dist(a, b):
            if a == 26: return 0
            return abs(a // 6 - b // 6) + abs(a % 6 - b % 6)
        dp = {26: 0}
        
        for i in range(len(word) - 1):
            curr_idx = ord(word[i]) - ord("A")
            next_idx = ord(word[i+1]) - ord("A")
            new_dp = {}
            d_move = get_dist(curr_idx, next_idx)
            for other, cost in dp.items():
                if other not in new_dp or new_dp[other] > cost + d_move:
                    new_dp[other] = cost + d_move
                d_other = get_dist(other, next_idx)
                if curr_idx not in new_dp or new_dp[curr_idx] > cost + d_other:
                    new_dp[curr_idx] = cost + d_other
            dp = new_dp
            
        return min(dp.values())
```
