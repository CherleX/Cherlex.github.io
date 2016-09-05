---
layout: post
title:  "maxnum depth of binary tree"
categories: LeetCode
tags:  LeetCode Tree
---

* content
{:toc}
二叉树最大高度

# [LeetCode 104 Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) #


> Given a binary tree, find its maximum depth.
> The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.


## recursive ##

```Python
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root == None:
            return 0
        return 1 + max(self.maxDepth(root.left),self.maxDepth(root.right))

```

## BFS ##
```Python
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        depth = 0
        level = [root] if root else []
        while level:
			depth += 1
			queue = []
			for lev in level:
				if lev.left:
					queue.append(lev.left)
				if lev.right:
					queue.append(lev.right)
			level = queue
        return depth
```
