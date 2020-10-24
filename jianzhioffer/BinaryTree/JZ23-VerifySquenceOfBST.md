# 题目描述

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则返回true,否则返回false。假设输入的数组的任意两个数字都互不相同。

# 解答：递归

已知条件：后序序列最后一个值为root；二叉搜索树左子树值都比root小，右子树值都比root大。

* 确定root；
* 遍历序列（除去root结点），找到第一个大于root的位置，则该位置左边为左子树，右边为右子树；
* **遍历右子树，若发现有小于root的值，则直接返回false；**
* 分别判断左子树和右子树是否仍是二叉搜索树（即递归步骤1、2、3）。

```python
class Solution:
    def VerifySquenceOfBST(self, sequence):
        # write code here
        if not sequence:
            return False    # 注意这里返回False
        return self.helper(sequence)   # 采用一个辅助函数进行判断的原因是在于，对于sequence为空的处理不同
    
    def helper(self, sequence):
        if not sequence:
            return True    # 注意这里返回True，说明前面的元素都满足条件
        root = sequence[-1]
        for i in range(len(sequence)):
            if sequence[i] > root:
                break
        for j in range(i, len(sequence)-1):
            if sequence[j] < root:
                return False
        return self.helper(sequence[:i]) and self.helper(sequence[i:-1])
```

# 感想

这道题自己做还是不太行，记住吧，继续加油！！！
