## LeetCode probem114.Flatten Binary Tree to Linked List

## 問題
[問題](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)

## 解法
```
class Solution:
    def flatten(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        cur = root
        while cur:
            if cur.left:
                prev = cur.left
                while prev.right:
                    prev = prev.right
                prev.right = cur.right
                cur.right = cur.left
                cur.left = None
            cur = cur.right
            
```

