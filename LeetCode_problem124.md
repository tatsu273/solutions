# LeetCode124. Binary Tree Maximum Path Sum
## 問題
[問題](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)
## 解法
```
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        res = -float('inf')
        def helper(node):
            if not node: return 0
            nonlocal res
            maxRight = max(0, helper(node.right))
            maxLeft = max(0, helper(node.left))
            res = max(res, maxLeft + node.val + maxRight)
            return max(maxLeft, maxRight) + node.val
        helper(root)
        return res
```
