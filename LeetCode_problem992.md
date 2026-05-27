## LeetCode Problem 992. Subarrays with K Different Integers
## 問題
[問題](https://leetcode.com/problems/subarrays-with-k-different-integers/submissions/1472498394/)
## 解法
```
class Solution:
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        left = 0
        right = 0
        cnt = 0
        res = 0
        nums_table = defaultdict(int)
        while right < len(nums):
            nums_table[nums[right]] += 1
            if len(nums_table) > k:
                cnt = 0
                nums_table[nums[left]] -= 1
                if nums_table[nums[left]] == 0:
                    del nums_table[nums[left]]
                left += 1
            while nums_table[nums[left]] > 1:
                nums_table[nums[left]] -= 1
                cnt += 1
                left += 1
            if len(nums_table) == k:
                res += cnt + 1
            right += 1
        return res

```
Time Complexity ... $O(N)$
Space Complexity ... $O(N)$
