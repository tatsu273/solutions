## LeetCode Problem198. House Robber
## 問題
[問題](https://leetcode.com/problems/house-robber/description/)
## 解法
```
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1: return nums[0]
        prev = nums[0]
        curr = max(nums[0], nums[1])
        for i in range(2, len(nums)):
            temp = curr
            curr = max(prev+nums[i], curr)
            prev = temp
        return curr
```
