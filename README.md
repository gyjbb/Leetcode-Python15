# Leetcode-Python15

## 110. Balanced Binary Tree

June 02, 2023  4h

Congratulations!\
This is the fifteenth day for leetcode python study. Today we will learn more about the Binary Tree!\
The challenges today are about ~~need to delete later~~.\
迭代法，大家可以直接过，二刷有精力的时候 再去掌握迭代法。


## 110. Balanced Binary Tree
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0110.%E5%B9%B3%E8%A1%A1%E4%BA%8C%E5%8F%89%E6%A0%91.md)\
[leetcode](https://leetcode.com/problems/balanced-binary-tree/)\
[video](https://www.bilibili.com/video/BV1Ug411S7my/?spm_id_from=333.788&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
平衡二叉树 （优先掌握递归）\
再一次涉及到，什么是高度，什么是深度，可以巩固一下。\
平衡二叉树定义为：一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。
```python
# ways 1: recursion:
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        if self.get_height(root) != -1:
            return True
        else:
            return False
        
    def get_height(self, root: TreeNode) -> int:
        if not root:        #base case
            return 0
        if (left_height:=self.get_height(root.left)) == -1:   #left
            return -1
        if (right_height:=self.get_height(root.right)) == -1:  #right
            return -1
        if abs(left_height-right_height) > 1:       #middle
            return -1
        else: 
            return 1+max(left_height, right_height)
```
```python
# ways 1: recursion simple version
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        return self.get_hight(root) != -1
    def get_hight(self, node):
        if not node:
            return 0
        left = self.get_hight(node.left)
        right = self.get_hight(node.right)
        if left == -1 or right == -1 or abs(left - right) > 1:
            return -1
        return max(left, right) + 1
```

## 257. 
二叉树的所有路径 （优先掌握递归）  
第一次接触到**回溯**的过程




## 404.
左叶子之和 （优先掌握递归）\
搞清楚什么是左叶子，剩下的就是二叉树的基本操作。
