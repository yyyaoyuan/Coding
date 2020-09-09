# 题目描述
请实现两个函数，分别用来序列化和反序列化二叉树。

二叉树的序列化是指：把一棵二叉树按照某种遍历方式的结果以某种格式保存为字符串，从而使得内存中建立起来的二叉树可以持久保存。序列化可以基于先序、中序、后序、层序的二叉树遍历方式来进行修改，序列化的结果是一个字符串，序列化时通过 某种符号表示空节点（#），以 ！ 表示一个结点值的结束（value!）。

二叉树的反序列化是指：根据某种遍历顺序得到的序列化字符串结果str，重构二叉树。

例如，我们可以把一个只有根节点为1的二叉树序列化为"1,"，然后通过自己的函数来解析回这个二叉树。

# 解答一

按照前序遍历的方式进行序列化以及反序列化。

```python
class Solution:
    def Serialize(self, root):
        # write code here
        if not root:
            return '#'
        return str(root.val) + '!' + self.Serialize(root.left) + '!' + self.Serialize(root.right)
    
    def Deserialize(self, s):
        # write code here
        l = s.split('!')
        return self.deserializeTree(l)
    
    def deserializeTree(self, l):
        if not l:
            return None
        val = l.pop(0)
        root = None
        if val != '#':
            root = TreeNode(int(val))
            root.left = self.deserializeTree(l)
            root.right = self.deserializeTree(l)
        return root
```
