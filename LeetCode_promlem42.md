## LeetCode Problem 42. Trapping Rain  Water
## 問題
[問題](https://leetcode.com/problems/trapping-rain-water/)
## 解法
```
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        left, right = 0, n-1
        leftMax = rightMax = 0
        total = 0
        while left < right:
            leftMax = max(leftMax, height[left])
            rightMax = max(rightMax, height[right])
            if leftMax < rightMax:
                total += leftMax - height[left]
                left += 1
            else:
                total += rightMax - height[right]
                right -= 1
        return total
```
