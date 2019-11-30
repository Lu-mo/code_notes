# leetcode 230 二叉搜索树中第k小元素 中等
[二叉搜索树中第k小元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)
## 全局变量计数,中序遍历
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        global count
        count = 0
        def recur(node):
            global count
            if node == None:
                return None
            else:
                val1 = recur(node.left)
                count += 1
                #print(count)
                if count == k:
                    return node.val
                val2 = recur(node.right)
                return val1 if val1 != None else val2
        
        return recur(root)
```
