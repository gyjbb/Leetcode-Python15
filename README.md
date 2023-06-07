# Leetcode-Python15

## 110. Balanced Binary Tree, 257. Binary Tree Paths， 404. Sum of Left Leaves

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
平衡二叉树定义为：一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。\
Recursion 3 steps:
1. 明确递归函数的参数和返回值。参数：当前传入节点。 返回值：以当前传入节点为根节点的树的高度。
2. 明确终止条件。递归的过程中依然是遇到空节点了为终止，返回0，表示当前节点为根节点的树高度为0。
3. 明确单层递归的逻辑。如何判断以当前传入节点为根节点的二叉树是否是平衡二叉树呢？当然是其左子树高度和其右子树高度的差值。\
分别求出其左右子树的高度，然后如果差值小于等于1，则返回当前二叉树的高度，否则返回-1，表示已经不是二叉平衡树了。
> int leftHeight = getHeight(node->left); // 左\
> if (leftHeight == -1) return -1;  // 如果左子树为-1，表示其下左右子树高度差大于1，不是平衡二叉树，则整个二叉树也已经不是平衡二叉树了。\
> int rightHeight = getHeight(node->right); // 右\
> if (rightHeight == -1) return -1;\
> int result;\
> // 中\
> if (abs(leftHeight - rightHeight) > 1) { result = -1;} // 一个节点下的左右子树高度差大于1，不是二叉树，向上返回-1，即这个节点值为-1.\
> else {result = 1 + max(leftHeight, rightHeight);} // 以当前节点为根节点的树的最大高度\
> return result;


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

## 257. Binary Tree Paths
[leetcode](https://leetcode.com/problems/binary-tree-paths/)\
二叉树的所有路径 （优先掌握递归），第一次接触到**回溯**的过程。
```python
# ways 1: recursion+回溯
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def traversal(self, cur, path, result):
        path.append(cur.val)   #middle
        if not cur.left and not cur.right: #reach the leaf node
            sPath = '->'.join(map(str, path))
            result.append(sPath)
            return
        if cur.left:    #left
            self.traversal(cur.left, path, result)
            path.pop()  #回溯一下
        if cur.right:   #riight
            self.traversal(cur.right, path, result)
            path.pop()  #回溯一下

    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        result = []
        path = []
        if not root:
            return result
        self.traversal(root, path, result)
        return result
```
```python
# ways 2: recursion
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        if not root:
            return []
        result = []
        self.traversal(root, [], result)
        return result
    
    def traversal(self, cur:TreeNode, path: List[int], result: List[str])-> None:
        if not cur:
            return
        path.append(cur.val)
        if not cur.left and not cur.right:
            result.append('->'.join(map(str,path)))
        if cur.left:
            self.traversal(cur.left, path[:], result)
        if cur.right:
            self.traversal(cur.right, path[:], result)
```

## 404. Sum of Left Leaves
[leecode](https://leetcode.com/problems/sum-of-left-leaves/)\
左叶子之和 （优先掌握递归）\
搞清楚什么是左叶子(是叶子节点，且是其父节点的左孩子），剩下的就是二叉树的基本操作。\
递归三部曲：\
1.确定递归函数的参数和返回值\
2.确定终止条件： 遍历到空节点，或者遍历到叶子节点了\
3.确定单层递归的逻辑:\
当遇到左叶子节点的时候，记录数值，然后通过递归求取左子树左叶子之和，和 右子树左叶子之和，相加便是整个树的左叶子之和。
```python
# ways 1: recusion:
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        if root is None:    #遍历到空节点，终止
            return 0
        #遍历到叶子结点，其子叶为null，也终止
        if root.left is None and root.right is None:
            return 0
        
        leftValue = self.sumOfLeftLeaves(root.left) #left
        #左子树是左子叶的情况
        if root.left and not root.left.left and not root.left.right:
            leftValue = root.left.val
        
        rightValue = self.sumOfLeftLeaves(root.right) #right

        sum_val = leftValue + rightValue    #middle
        return sum_val
```
```python
# ways 1: recusion simple version:
class Solution:
    def sumOfLeftLeaves(self, root):
        if root is None:
            return 0
        leftValue = 0
        if root.left is not None and root.left.left is None and root.left.right is None:
            leftValue = root.left.val
        return leftValue + self.sumOfLeftLeaves(root.left) + self.sumOfLeftLeaves(root.right)
```


