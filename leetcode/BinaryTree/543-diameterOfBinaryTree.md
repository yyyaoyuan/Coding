# 二叉树的直径

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。

# 解答：深度优先遍历

* 任意一个节点的直径为：左子树深度+右子树深度
* 利用一个全局变量self.res维护当前最长的直径
* 对所有节点的左，右子树求深度

```python
class Solution:
     def __init__(self):
         self.res = 0
         
     def diameterOfBinaryTree(self, root):
         self.depth(root)
         return self.res
         
     def depth(self, node):
         if not node:
            return 0
         left = self.depth(node.left)
         right = self.depth(node.right)
         self.res = max(self.res, left+right)
         return max(left, right) + 1
```

# 感想

这是第一次做在二叉树中深度优先遍历的题，和之前做深度优先遍历题的套路类似，从根节点深度优先遍历，然后利用一个全局变量记录当前最长的直径，最后返回最长的直径。
