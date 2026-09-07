## LeetCode problems 1320. Minimum Distance to Type a Word Using Two Fingers
## 問題
[問題](https://leetcode.com/problems/minimum-distance-to-type-a-word-using-two-fingers/description/)
## 解法
### 1. MultidimentionalDP
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
Time Complexity ... $O(N)$ <br>
Space Complexity ... $O(26\*26\*N) = O(N)$

### 解説
全探索ですべての動かし方を探索すると時間計算量が
$O(2^N)$
になってしまいます。<br>
この問題は部分構造最適性を持ちます。これは以下のような特徴です。
- 部分問題も同じ最適化問題が成立している<br>
- 部分問題間が独立している<br>

この場合、動的計画法が利用できます。<br>
以下のように<br><br>
$dp[i] ... i$ 番目の文字を押すときの距離の最小値 <br><br>
とテーブルを定めた場合、次の
$i+1$
文字目の処理を行う場合の移動距離が分かりません。そこで、以下のように情報を加えてテーブルを定義します。<br><br>
$dp[i][j][k] ... i$ 番目の文字を押すときに2本の指がぞれぞれ
$j, k$
番目の文字を押している場合の距離の最小値<br><br>
これによりそれぞれの部分問題で最小値が計算できるようになります。

### 2. DP
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

Time Complexity ... $O(N)$ <br>
Space Complexity ... $O(26) = O(1)$

### 解説
1つ目の解法では3次元dpを利用して解きましたが、これはメモリの消費量が大きくなってしまうというデメリットを持ちます。<br>
そこで、

